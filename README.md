# jm-electron-app-v3.1 Monorepo

This is a monorepo for Electron applications, packages, and tooling, managed with [pnpm](https://pnpm.io/) workspaces and [Turbo](https://turbo.build/). It provides a modern, type-safe, and maintainable development environment for building Electron apps and supporting libraries.

## Features

- **Modular Structure:** Organizes code into `apps`, `packages`, and `tooling` for clear separation of concerns.
- **TypeScript-first:** All code is written in TypeScript for safety and developer experience.
- **Automated Formatting & Linting:** Uses Prettier with sort-package-json integration and ESLint.
- **Dependency Management:** Automated consistency checks with [Sherif](https://github.com/wobsoriano/sherif) and [syncpack](https://github.com/JamieMason/syncpack).
- **Task Orchestration:** [Turbo](https://turbo.build/) for fast, cached, and parallel task execution across workspaces.
- **Modern Tooling:** Includes Vite for fast builds, Vitest for testing, and comprehensive development utilities.

## Getting Started

### Prerequisites

- **Node.js**: >=22
- **pnpm**: >=10

### Install Dependencies

```sh
pnpm install
```

### Update Dependencies

Check for updates:

```sh
pnpm deps:check
```

Verify everything still works:

```sh
pnpm deps:verify
```

Fix version inconsistencies:

```sh
pnpm sync:versions
```

The workflow provides:

- Automated checks on schedule or manual trigger
- Renovate PRs for all dependency updates with proper grouping
- Monorepo health verification with typecheck and tests
- Version consistency validation via syncpack

### Common Scripts

All scripts are run from the root and apply recursively to all workspaces using Turbo:

| Script                  | Description                                               |
| ----------------------- | --------------------------------------------------------- |
| `pnpm app:dev`          | Start the Electron app in development mode                |
| `pnpm app:start`        | Start the Electron app                                    |
| `pnpm app:test`         | Run app tests in watch mode                               |
| `pnpm build`            | Build all apps, packages, and tooling                     |
| `pnpm clean`            | Clean all build artifacts, caches, logs, and node_modules |
| `pnpm clean:workspaces` | Clean build artifacts in all workspaces                   |
| `pnpm deps:check`       | Check for outdated packages interactively                 |
| `pnpm deps:interactive` | Interactively select and update packages                  |
| `pnpm deps:latest`      | Update all packages to their latest versions              |
| `pnpm deps:update`      | Update packages to latest available versions              |
| `pnpm deps:verify`      | Verify monorepo health: lint, typecheck, and test         |
| `pnpm dev`              | Start development mode with watch and hot reload          |
| `pnpm format`           | Check code formatting with Prettier                       |
| `pnpm format:fix`       | Auto-fix code formatting with Prettier                    |
| `pnpm format:pkg`       | Sort all package.json files                               |
| `pnpm lint`             | Run ESLint checks across all workspaces                   |
| `pnpm lint:fix`         | Auto-fix lint issues across all workspaces                |
| `pnpm lint:repo`        | Run Sherif to check monorepo dependency consistency       |
| `pnpm sync:lint`        | Check version consistency with syncpack                   |
| `pnpm sync:versions`    | Fix version mismatches across workspaces                  |
| `pnpm test`             | Run tests across all workspaces                           |
| `pnpm test:watch`       | Run tests in watch mode                                   |
| `pnpm typecheck`        | Validate TypeScript typings across all workspaces         |

### Directory Structure

```
/
├── apps/         # Electron applications and playgrounds
├── packages/     # Shared libraries and utilities
├── tooling/      # Shared configuration and build tools
├── turbo/        # Turbo generators and configuration
├── logs/         # Application logs
└── pnpm-workspace.yaml
```

## Packages

This monorepo includes the following packages:

### Core Utilities

- **[@jm-monorepo/config-provider](./packages/config-provider/README.md)** - Advanced configuration loader with support for multiple formats (.js, .ts, .json, .yaml, .toml), RC files, environment-specific configs, and hot reload
- **[@jm-monorepo/debug](./packages/debug/README.md)** - Tiny debugging utility with namespace-based filtering, performance tracking, and colorized output
- **[@jm-monorepo/logger](./packages/logger/README.md)** - Comprehensive Pino-based logging solution with environment-aware configurations, file rotation, and error handling
- **[@jm-monorepo/node-utils](./packages/node-utils/README.md)** - Collection of utilities for arrays, objects, strings, filesystem operations, and path manipulation

### Build & Development Tools

- **[@jm-monorepo/electron-vite](./packages/electron-vite/README.md)** - Vite-based toolkit for building Electron applications with custom plugins and development utilities
- **[@jm-monorepo/package-json-utils](./packages/package-json-utils/README.md)** - TypeScript utilities for reading, validating, and manipulating package.json files

### File & Path Utilities

- **[@jm-monorepo/find-file-by-name](./packages/find-file-by-name/README.md)** - Powerful file search utility with sync/async APIs, traversal patterns, and monorepo-friendly boundary controls

### Stream Utilities

- **[@jm-monorepo/callback-stream](./packages/callback-stream/README.md)** - Safe variant of concat-stream that returns an array of streamed data
- **[@jm-monorepo/end-of-stream](./packages/end-of-stream/README.md)** - Calls a callback when readable/writable/duplex streams complete or fail
- **[@jm-monorepo/once](./packages/once/README.md)** - Ensures a function is called only once with support for strict mode
- **[@jm-monorepo/pump](./packages/pump/README.md)** - Pipes streams together and destroys all on close with callback support
- **[@jm-monorepo/split2](./packages/split2/README.md)** - Stream splitter that breaks up streams and reassembles by line (newline delimited JSON support)

### Logging Transports & Tools

- **[@jm-monorepo/pino-abstract-transport](./packages/pino-abstract-transport/README.md)** - Framework for writing custom Pino transports with ease
- **[@jm-monorepo/pino-test-util](./packages/pino-test-util/README.md)** - Testing utilities for Pino logging

### Data & Object Utilities

- **[@jm-monorepo/fast-copy](./packages/fast-copy/README.md)** - Blazing fast deep object copier with circular reference support and 2x faster than alternatives
- **[@jm-monorepo/fast-safe-stringify](./packages/fast-safe-stringify/README.md)** - Safe and fast serialization alternative to JSON.stringify with circular reference protection
- **[@jm-monorepo/secure-json-parse](./packages/secure-json-parse/README.md)** - Secure JSON.parse alternative that protects against prototype pollution attacks

### Terminal & Display

- **[@jm-monorepo/colorize-terminal](./packages/colorize-terminal/README.md)** - Lightweight terminal color and style support with ANSI codes (standard, 256-color, and true color) and intelligent color detection
- **[@jm-monorepo/table-in-terminal](./packages/table-in-terminal/README.md)** - Create beautifully formatted tables in the terminal with rich styling, spanning, and hyperlink support

### Helpers

- **[@jm-monorepo/ms](./packages/ms/README.md)** - Convert various time formats to milliseconds and vice versa

## Tooling & Conventions

- **Task Runner:** [Turbo](https://turbo.build/) for fast, cached builds and parallel execution
- **Package Manager:** [pnpm](https://pnpm.io/) with workspace support
- **Formatting:** [Prettier](https://prettier.io/) with custom configuration
- **Linting:** [ESLint](https://eslint.org/) with flat config
- **Dependency Management:** [Sherif](https://github.com/wobsoriano/sherif) for monorepo consistency, [syncpack](https://github.com/JamieMason/syncpack) for version management
- **Type Checking:** [TypeScript](https://www.typescriptlang.org/) with strict mode
- **Build Tool:** [Vite](https://vitejs.dev/) for fast builds and HMR
- **Testing:** [Vitest](https://vitest.dev/) for unit and integration tests
- **Monorepo Tools:** [@manypkg/cli](https://github.com/Thinkmill/manypkg) for workspace validation

## License

MIT © Johan Meester
