# When a cached None value was mistaken for a missing key

**Donatus Gwer · 13 October 2026 · [Upstream PR #851](https://github.com/jazzband/django-redis/pull/851)**

A cache can store `None` as a real value. For example, an application can cache an empty lookup result so repeated requests do not keep querying the database. Changing that entry's cache version should move the existing value. In django-redis, it instead raised a missing-key error.

## Reproduce the failure

Using an isolated Redis instance and the normal Django cache interface:

```python
cache.set("cached-none", None, version=2)
assert cache.has_key("cached-none", version=2) is True
cache.incr_version("cached-none", version=2)
# Before the fix: ValueError reporting that the key was not found
```

Both DefaultClient and ShardClient fetched the old entry with `get()` and checked `if value is None`. That conflated a stored `None` with the default result for an absent key. Redis still contained the original key; this was a client-side distinction error.

## Make the distinction explicit

The fix gives each call a unique missing-value sentinel:

```python
missing = object()
value = self.get(old_key, default=missing, version=version, client=client)
if value is missing:
    raise ValueError(...)
```

The sentinel is returned only on a miss; it is never stored in Redis. A cached `None` can now follow the existing version-change path. The patch changes both clients and retains the missing-key error. It adds no Redis round trip and does not change the public API.

## Test the behavior across cache configurations

The regression verifies that the old version disappears, the new version exists, and reading the new version with a non-None default returns the stored `None`. It covers positive and negative version deltas and finite and persistent expiration. A separate test confirms genuinely absent keys still raise an error without creating a new version.

The existing configuration matrix includes default and sharded clients, HerdClient, Sentinel, JSON/MessagePack serializers, compression and a Unix socket. Each configuration was also exercised in its own pytest process, avoiding reliance on process-global Django settings switching correctly within one run.

| Check | Recorded result |
|---|---|
| Cached-None regression on unchanged baseline | 48 failures across 12 separately executed configurations |
| Same regression after the fix | 48 passes |
| Missing-key regression | 12 passes in separate processes |
| Full repository suite | 2,065 passed; 7 skipped |
| Repository-configured line coverage | 72.9% |
| Formatting and lint | All pre-commit hooks passed; Ruff 0.15.15 |
| Type checking | mypy passed for 27 source files |

The full suite ran with Python 3.14.8, Django 6.0.9, redis-py 8.1.0 and Redis 8.0.2. Redis, Sentinel and the Unix socket lived inside a disposable container with no published ports. Existing application caches were not used or cleared.

## Scope and upstream status

This is a small correctness fix. It does not make version changes atomic, resolve unrelated concurrent cache writes, or change HerdClient's existing TTL extension behavior. The full upstream Python/Django matrix was not reproduced locally.

The PR is **submitted, not merged**. As checked on 13 October 2026, pre-commit.ci passed; GitHub Actions still requires maintainer approval for a first-time contributor. No human maintainer review has arrived. AI assistance was used for investigation, implementation and verification, and disclosed in the PR.

[Review the patch and tests](https://github.com/jazzband/django-redis/pull/851/files) · [Upstream Actions approval state](https://github.com/jazzband/django-redis/actions/runs/38325063053) · [Back to profile](../README.md)
