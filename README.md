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
| hostfs | [asubbarao/hostFS](https://github.com/asubbarao/hostFS/tree/duckdb-2.0) at `c60bbc1`: [gropaul/hostFS](https://github.com/gropaul/hostFS) `29017b2` ported to the DuckDB 2.0 API, with its bundled ghc::filesystem retrying `opendir`/`readdir`/`read` only on a failed EINTR (as upstream ghc now does) | MIT, see `LICENSE-hostfs` |
| quackapi | [asubbarao/quackapi](https://github.com/asubbarao/quackapi) `c0260c2` on `osx_arm64`, `osx_amd64`, `linux_amd64` and `linux_arm64`, each the artifact of that commit's extension-ci-tools run (45450809950), signed here. It includes `quackapi_selfdispatch`; community serves older `afc31ea` for 2.0 | the quackapi repository's license |
| sitting_duck | [teaguesterling/sitting_duck](https://github.com/teaguesterling/sitting_duck) `67e6381` plus commit `caaf3fc`, which adds a `tsx` language parsed with tree-sitter-typescript's tsx grammar (`.tsx` was parsed with the typescript grammar, so JSX came out as ERROR nodes). The commit is not yet published or proposed upstream | Apache-2.0, see `LICENSE-sitting_duck` and `NOTICE-sitting_duck` |

Platforms: `osx_arm64` (built on the Mac) and `linux_amd64` (built by each source repository's extension-ci-tools workflow, then
signed here), so duckstack's boot check runs on Linux. quackapi also has `osx_amd64` and `linux_arm64`. sitting_duck is
`osx_arm64` only for now.
