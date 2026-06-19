# Contributing to Vortex

First off — thank you for taking the time to contribute! Vortex is an open-source
protocol, and we welcome issues, pull requests, and discussion from anyone.

This project participates in the [Drips](https://www.drips.network/) ecosystem for
sustainable open-source funding. Merged contributions to this repository may be
recognized as part of our dependency/contributor funding splits, so contributing
here is meaningful beyond the code itself.

---

## Code of Conduct

This project and everyone participating in it is governed by our
[Code of Conduct](./CODE_OF_CONDUCT.md). By participating, you are expected to
uphold it. Please report unacceptable behavior to the maintainers.

---

## Repositories

Vortex is split across independent repositories under the
[`vortex-protocol`](https://github.com/vortex-protocol) organization:

| Repo | Stack | Description |
|---|---|---|
| [`vortex-contract`](https://github.com/vortex-protocol/vortex-contract) | Rust / Soroban | On-chain intent settlement contracts |
| [`vortex-backend`](https://github.com/vortex-protocol/vortex-backend)  | TypeScript / Express | Intent relay API + WebSocket feed |
| [`vortex-frontend`](https://github.com/vortex-protocol/vortex-frontend) | TypeScript / Next.js 14 | Swap UI + solver portal |

Each repository is independently buildable. See each repo's `README.md` for setup.
This file lives in the org-wide
[`.github`](https://github.com/vortex-protocol/.github) repository and applies to
all of them.

---

## Getting Started

1. **Fork** the repository and clone your fork.
2. Create a branch from `main`:
   ```bash
   git checkout -b feat/short-description
   ```
3. Make your changes (see [Development](#development) below).
4. Ensure lint, type-check, and the contract build pass locally.
5. Commit using [Conventional Commits](#commit-messages).
6. Push and open a pull request against `main`.

---

## Development

### Contract ([`vortex-contract`](https://github.com/vortex-protocol/vortex-contract))

```bash
cd vortex-contract/intent_settlement   # within a clone of the vortex-contract repo
cargo fmt --all
cargo clippy --all-targets -- -D warnings
cargo test
stellar contract build
```

### Backend ([`vortex-backend`](https://github.com/vortex-protocol/vortex-backend))

```bash
npm install
npm run lint
npm run build      # tsc type-check + emit
npm run dev
```

### Frontend ([`vortex-frontend`](https://github.com/vortex-protocol/vortex-frontend))

```bash
npm install
npm run lint
npm run build
npm run dev
```

---

## Commit Messages

We follow [Conventional Commits](https://www.conventionalcommits.org/):

```
feat(backend): add /api/v1/tokens registry endpoint
fix(contract): reject fill after deadline
docs: clarify solver bond slashing
chore(frontend): bump next to 14.2.3
```

Common types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`.

---

## Pull Request Guidelines

- Keep PRs focused — one logical change per PR.
- Reference the issue it closes (e.g. `Closes #12`).
- Include a clear description of *what* changed and *why*.
- Add or update tests where it makes sense.
- Make sure CI is green before requesting review.
- For UI changes, include a screenshot or short clip.

---

## Finding Something to Work On

- Issues labeled **`good first issue`** are scoped for newcomers.
- Issues labeled **`help wanted`** are ready for community pickup.
- Each repo's `README.md` lists larger initiatives on its roadmap.

If you want to work on something not yet tracked, open an issue first so we can
align on the approach before you invest time.

---

## Reporting Bugs & Security Issues

- For regular bugs, open a bug report on the relevant repo (the
  [shared template](./ISSUE_TEMPLATE/bug_report.md) applies org-wide).
- For **security vulnerabilities**, do **not** open a public issue — follow
  [SECURITY.md](./SECURITY.md) instead.

---

## License

By contributing, you agree that your contributions will be licensed under the
[MIT License](./LICENSE) that covers this project.
