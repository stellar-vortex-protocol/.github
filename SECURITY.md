# Security Policy

## Supported Versions

Vortex is pre-1.0 and under active development. Only the latest `main` branch
receives security fixes at this stage.

| Version | Supported |
|---------|-----------|
| `main`  | ✅        |
| < 0.1   | ❌        |

## Reporting a Vulnerability

**Please do not report security vulnerabilities through public GitHub issues,
discussions, or pull requests.**

Instead, report them privately using one of:

- [GitHub private vulnerability reporting](https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing-information-about-vulnerabilities/privately-reporting-a-security-vulnerability)
  (the **"Report a vulnerability"** button on the Security tab), or
- Email the maintainers at **security@vortex-protocol.dev**

Please include, as far as you are able:

- A description of the vulnerability and its impact
- Steps to reproduce or a proof of concept
- The affected component (`vortex-contract`, `vortex-backend`, `vortex-frontend`)
  and version/commit
- Any suggested remediation

## What to Expect

- We aim to acknowledge reports within **72 hours**.
- We will keep you informed as we investigate and work on a fix.
- We will credit reporters in the release notes unless you prefer to remain
  anonymous.
- Please give us reasonable time to remediate before public disclosure.

## Scope

Because Vortex handles user funds via on-chain solver bonds and settlement, we
are especially interested in:

- Smart-contract logic errors (bond accounting, slashing, intent lifecycle)
- Authorization bypass in the settlement contract or relay API
- Fund-loss or fund-lock conditions
- Denial-of-service against the relay or settlement layer

Thank you for helping keep Vortex and its users safe.
