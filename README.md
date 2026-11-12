# duckdb-extensions

A signed DuckDB 2.0 extension repository: the builds duckstack boots, where community has no DuckDB 2.0 build
or serves an older one.
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
| hostfs | osx_arm64: [gropaul/hostFS](https://github.com/gropaul/hostFS) at `29017b2` with a local 2.0 patch. linux_amd64: [asubbarao/hostFS](https://github.com/asubbarao/hostFS/tree/duckdb-2.0) at `8f1e7d7`, the same release ported to the DuckDB 2.0 API | MIT, see `LICENSE-hostfs` |
| quackapi | [asubbarao/quackapi](https://github.com/asubbarao/quackapi) at `2b2f1d9` (has `quackapi_selfdispatch`; community serves the older `afc31ea` for 2.0) | the quackapi repository's license |
| toml | [asubbarao/duckdb-toml](https://github.com/asubbarao/duckdb-toml/tree/duckdb-2.0-read-toml) at `a2cac97`: [vergenzt/duckdb-toml](https://github.com/vergenzt/duckdb-toml) `263bc5a` built for DuckDB 2.0.0, plus `read_toml(path or glob)` | MIT, see `LICENSE-toml` |

Platforms: `osx_arm64` (built on the Mac) and `linux_amd64` (built by each source repository's extension-ci-tools workflow, then
signed here), so duckstack's boot check runs on Linux.
