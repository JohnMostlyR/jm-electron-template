# AGENTS.md for this monorepo

## Project Overview

This is a modern, type-safe monorepo for building Electron applications with React and TypeScript. It provides a comprehensive development environment with multiple reusable packages including logging, configuration management, stream utilities, and terminal display tools. The project uses pnpm workspaces and Turborepo for efficient dependency management and fast, cached builds across all packages.

The monorepo is designed to support enterprise-grade Electron applications with features like automated formatting, linting, testing, database management with Drizzle ORM, internationalization support, and comprehensive logging infrastructure using Pino.

---

## Technology Stack

- Language: **TypeScript**
- Runtime: **Node.js**
- Package Manager: **pnpm**
- Build System: **Turborepo**

---

## Core Commands

### For all workspaces (run from root)

- Run the Turborepo **lint** task: `pnpm lint`
- Run the Turborepo **lint** task with auto-fix: `pnpm lint:fix`
- Run the Turborepo **format** task: `pnpm format`
- Run the Turborepo **format** task with the write option: `pnpm format:fix`
- Run the Turborepo **typecheck** task: `pnpm typecheck`
- Run the Turborepo **test** task: `pnpm test`
- Run the Turborepo **test** task in watch mode: `pnpm test:watch`
- Run the Turborepo **build** task: `pnpm build`
- Run the Turborepo **clean** task: `pnpm clean:workspaces`

### For a specific workspace (run from root)

- Use the pnpm filter option (`pnpm --filter <package_selector> <command>`)

**IMPORTANT**: Use the pnpm 'filter' option to focus on a specific package (from the _root_ of this monorepo). Make sure to check the name property in the local package.json.

### For maintenance on this monorepo

- Update dependencies: `pnpm deps:update`
- Verify updated dependencies: `pnpm deps:verify`
- Clean all build artifacts and node_modules: `pnpm clean:workspaces`

---

## Project Structure

This is a Turbo monorepo with the following layout:

- `/.config/*`: Shared configurations
- `/apps/*`: End-user applications
- `/packages/*`: Shared libraries
- `/tooling/*`: Shared tooling
- `/turbo/*`: Turbo generators

Guidelines:

- Apps may depend on packages
- Packages **must not** depend on apps
- Cross-package dependencies must be explicit in `package.json`
- Shared configurations must be stored in the `/.config/` folder and consumed via the `@jm-monorepo/config-provider` package **wherever** this is supported and practical. (e.g. `.gitignore`, `.prettierignore`, `.env` etc. need to be in the root folder)

---

## General Coding Rules

**IMPORTANT:**

- Prefer **explicit, readable code** over clever abstractions
- Avoid unnecessary dependencies
- Do not introduce breaking changes without documentation
- New code must be [tested](#testing)
- Do not modify public APIs without updating:
  - Types
  - Tests
  - Relevant documentation (e.g. `JSDoc`, `README.md`, `AGENTS.md`)
- **[VALIDATION CHECKPOINT]** After creating, or making changes to, any code...
  - Run `pnpm lint` and fix any errors until all errors are resolved
  - Run `pnpm format`
  - Run `pnpm typecheck` and fix any errors until all errors are resolved
  - Run `pnpm test` and fix any errors until the whole suite is green
  - Run `pnpm coverage` and and aim for 80%+ coverage
  - Repeat all these steps until all issues are solved
- **[DOCUMENT CHECKPOINT]** After creating, or making changes to, any code...
  - Update the nearest README.md
  - Update the nearest AGENTS.md
- **[CLEANUP CHECKPOINT]** Before completing any task, delete all temporary files you created
  - Any file created for debugging, testing, or investigation purposes
  - Examples: `test-output.txt`, `debug.log`, `*.temp`, `*.tmp`, `scratch.*`, helper scripts
  - Check both root and subdirectories (packages/_, apps/_, tooling/\*)
  - Files used for investigation but not part of the codebase
  - Use `file_search` to verify no temporary files remain before task completion

---

## TypeScript Conventions

- Prefer interfaces/types already defined in shared packages
- Export types explicitly
- Put shared types in a separate `types.ts`

---

## Testing

**IMPORTANT:**

- Never run Vitest with the option `--passWithNoTests` or `--pass-with-no-tests`
- Use best practices as described in `.agents/docs/testing-best-practices.md`!.
- New behavior should include tests where practical
- Do not delete tests unless the behavior is removed intentionally
- Keep tests deterministic and isolated
- Use the `describe-it` pattern consistently with existing patterns.
- The name of a test must start with 'should' so it reeds like it-should
- Do not add tests to the wrong test suite (e.g., adding to end of file instead of inside relevant suite).

---

## Documenting

- Avoid the use of abbreviations, _unless_ commonly used by the intended audience

### Comments

- Use JSDoc style comments for `functions`, `interfaces`, and `classes`.

### Common rules for markdown and JSDoc

- Use `shell` for example code that runs in the command-line interface.

  Example:

  ```shell
  pnpm add -D prettier
  ```

- Do not sound like a salesman by avoiding words like 'comprehensive' and 'powered' as much as possible.

---

## Versioning & Changes

- Follow semantic versioning for packages
- Update changelogs or release notes when required
- Avoid combining unrelated changes in a single commit

---

## Safety Rules for Automated Changes

Automated agents must:

- Make the smallest possible change to achieve the goal
- Avoid large refactors unless explicitly requested
- Never remove code without understanding its usage
- Preserve backward compatibility unless instructed otherwise
- Never loosen or override any rules as stated in `eslint.config.js`
- Prevent the need to loosen or override any linting rule with directives.
  Common exceptions are:
  - The use of the `any` type were it is common (e.g. `chunks` in streams)
  - The `max-param` rule where it would otherwise make the code less readable
  - Too expensive to change in an older codebase
- Never loosen any rules as stated in `tsconfig.json` **without** asking

If uncertain, **stop and ask for clarification**.

---

## Source of Truth

If this document conflicts with:

- Package-level `AGENTS.md`
- Existing code patterns

Then:

1. Package-level `AGENTS.md` wins for that package
2. Existing code patterns win over assumptions
