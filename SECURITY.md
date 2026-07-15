# Security Policy

The maintainers of Open Defense Cloud take the security of our products
seriously and appreciate your efforts to responsibly disclose your findings.

## Supported Versions

Security fixes are shipped **"fail forward"**: a fix is released in the next version,
and users are expected to upgrade to receive it. Only the **latest released version**
of each product receives security fixes; older versions are not patched or
backported.

## Reporting a Vulnerability

Please report security vulnerabilities privately using **GitHub Private Vulnerability
Reporting**. Open the **Security** tab of the affected repository and click
**"Report a vulnerability"** (the direct URL is
`https://github.com/opendefensecloud/<repository>/security/advisories/new`).
If you are unsure which repository is affected, report against the most likely one
and the maintainers will route it.

Please do **not** report security vulnerabilities through public GitHub issues,
pull requests, or discussions.

Please include as much detail as possible: affected component and version, a
description of the issue, reproduction steps or a proof of concept, and the
potential impact.

## Scope

In scope are vulnerabilities in the code and released artifacts (container images,
Helm charts, binaries) of Open Defense Cloud products, including their APIs, web
UIs, and controllers/agents.

## Out of Scope

The following are generally **not** considered reportable vulnerabilities:

- Insecure configuration chosen by the operator/user (i.e., not the shipped default).
- Reports from automated dependency scanners **without** a demonstrated, exploitable
  path against the product. Please include proof that the reported CVE is actually
  reachable and exploitable in our context.

## Coordinated Disclosure

We ask security researchers to practice
[coordinated vulnerability disclosure](https://cheatsheetseries.owasp.org/cheatsheets/Vulnerability_Disclosure_Cheat_Sheet.html).
In return, the maintainers pledge to engage in good faith, keep you informed of
progress, and credit you (if you wish) when the fix is published. We coordinate the
timing of public disclosure with the reporter. The maintainers own CVE assignment
for confirmed vulnerabilities in Open Defense Cloud products and will request CVE IDs
as appropriate.

## Security Advisories

Advisories are published through GitHub Security Advisories on the affected
repository. Public disclosure of a vulnerability happens there once a fix is
available.
