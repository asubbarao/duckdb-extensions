# duckdb-extensions

A signed DuckDB 2.0 extension repository: extensions duckstack needs that have no DuckDB 2.0 build on community yet.
Each file is signed with this publisher key (fingerprint `sha256:451b1e602206b93df6d1f6377fdebbb0d2d257b4bdc7dee2dbee8085427a4b8f`).

```sql
SET allow_extension_repositories = 'allowed';
CREATE EXTENSION REPOSITORY duckstack_local
WITH PREFIX 'https://raw.githubusercontent.com/asubbarao/duckdb-extensions/main'
USING PUBLIC KEY '<key in asubbarao/duckstack server/local_repository.sql>';
INSTALL hostfs FROM duckstack_local;
LOAD hostfs;
```

| extension | source | license |
|---|---|---|
| hostfs | [gropaul/hostFS](https://github.com/gropaul/hostFS) at `29017b2`, built for DuckDB 2.0.0 | MIT, see `LICENSE-hostfs` |

Platforms: `osx_arm64`.
