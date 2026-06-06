# Hugging Face MCP Server

MCP server providing Hugging Face Hub tools — model search, dataset discovery, file management, Spaces, inference, and more. Supports stdio, streamable HTTP, and streamable HTTP JSON transports.

## Quick Reference

```bash
pnpm install                      # install workspace dependencies (Corepack-managed pnpm)
pnpm build                        # build all workspace packages
pnpm dev                          # watch MCP package + run server with HMR
pnpm start                        # start production server
pnpm lint                         # lint
pnpm typecheck                    # type-check
pnpm format                       # format
pnpm test                         # run all tests
pnpm -C packages/app test         # app package tests only
pnpm -C packages/mcp test         # mcp package tests only
pnpm run buildrun                 # clean → build → lint → test → start
```

## Project Structure

```
hf-mcp-server/
├── packages/
│   ├── app/        # MCP server + management web UI
│   │   ├── src/server/   # server code
│   │   ├── src/web/      # UI code
│   │   └── test/         # tests
│   ├── mcp/        # shared MCP tools/library
│   │   ├── src/          # source + co-located *.test.ts
│   │   └── test/         # additional tests
│   └── e2e-python/ # Python-based E2E harnesses
├── docs/           # documentation
├── docs-internal/  # internal docs
├── scripts/        # auxiliary scripts
├── spec/           # specifications
└── Dockerfile      # container image
```

## Coding Style

- TypeScript ESM throughout.
- Prettier: tabs (`useTabs: true`, `tabWidth: 2`), semicolons, single quotes, `printWidth: 120`.
- ESLint strict in `packages/mcp` and server code: no `any`, consistent type imports, prefer `interface`.
- Test files: `.test.ts` or `.spec.ts` naming.

## Configuration

Key environment variables:

| Variable | Description |
|---|---|
| `DEFAULT_HF_TOKEN` / `HF_TOKEN` | Hugging Face auth token |
| `TRANSPORT` | Server mode: `stdio` \| `streamableHttp` \| `streamableHttpJson` |

Never commit secrets. Add new env vars to `README.md`.

## Testing

- Unit/integration tests use Vitest in both `packages/app` and `packages/mcp`.
- Add tests for new tools, transports, or formatting logic.

## Commit Guidelines

- Small, descriptive commits with scope when helpful (`app`, `mcp`).
- Conventional-style messages: `chore: release vX`, `feat(mcp): add tool`.
- PRs: concise summary, test results, linked issue, screenshots for UI changes.
