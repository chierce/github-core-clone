# GitHub Core Clone Forge Engine

[![make.fun · github-core-clone-01](https://make.fun/badge/github-core-clone-01.svg)](https://make.fun/bounty/github-core-clone-01?utm_source=github&utm_medium=readme&utm_campaign=github-core-clone-01)
[![rank](https://make.fun/badge/github-core-clone-01/chierce/github-core-clone/rank.svg)](https://make.fun/bounty/github-core-clone-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=github-core-clone-01)
[![reward](https://make.fun/badge/github-core-clone-01/chierce/github-core-clone/reward.svg)](https://make.fun/bounty/github-core-clone-01?utm_source=github&utm_medium=readme&utm_campaign=github-core-clone-01)

A complete, high-performance GitHub-compatible Git forge implemented in pure standalone Node 22 TypeScript for make.fun competition [`github-core-clone-01`](https://make.fun/bounty/github-core-clone-01).

Supports the full Git Smart-HTTP protocol, GitHub REST API v3, GitHub GraphQL API v4, and Model Context Protocol (MCP) server endpoints with zero runtime dependencies.

## Features

- **Git Smart-HTTP**: Full Smart-HTTP implementation (`info/refs`, `git-upload-pack`, `git-receive-pack`) supporting clone, shallow fetch with generational `deepen`, unshallow traversal, push, OFS_DELTA and REF_DELTA pack generation and decompression.
- **GitHub REST API v3**: Repositories, branches, commit lineages, contents, tree blobs, issues, comments, labels, pull requests, and branch merge resolution.
- **GitHub GraphQL API v4**: Introspection schema, repository queries, viewer resolution, pull request and issue queries with file diff trees.
- **Model Context Protocol (MCP)**: Native JSON-RPC MCP server endpoints over streamable HTTP supporting tool enumeration and invocations (`create_issue`, `get_issue`, `create_pull_request`, etc.).
- **Zero Runtime Dependencies**: Runs entirely on native Node 22 (`--experimental-strip-types`) using built-in `node:http`, `node:crypto`, `node:zlib`, and `node:buffer`.

## Run it

```sh
node --experimental-strip-types main.ts
```

## The Surface

| Route | What it is |
| --- | --- |
| `GET /healthz` | 200 `{"ok":true}`: the env's boot probe |
| `GET /api/v3/` | 200, `X-Oauth-Scopes: repo, read:org`, JSON API root |
| `/api/v3/...` | GitHub REST v3: repositories, branches, commits, contents, issues, comments, labels, pull requests, files, merges |
| `POST /api/graphql` | GitHub GraphQL v4: introspection, viewer, repository queries |
| `POST /mcp` | Model Context Protocol over streamable HTTP: initialize, tools/list, tools/call |
| `/<owner>/<repo>.git/...` | Git Smart-HTTP: `info/refs`, `git-upload-pack`, `git-receive-pack` |

## License

MIT
