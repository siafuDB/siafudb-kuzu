# Security Policy

We take the security of Nyuchi Africa projects seriously. This
policy applies to every repository under the
[@nyuchi](https://github.com/nyuchi) GitHub organization unless
that repository ships its own `SECURITY.md` with different terms.

## Reporting a Vulnerability

**Please do not open a public issue, pull request, or discussion for a
suspected vulnerability.** Public disclosure before a fix is available
puts users at risk.

You have two private channels. Either is acceptable; use whichever you
prefer.

### 1. Email (preferred for first contact from outside GitHub)

Send a report to **<security@nyuchi.com>**.

If you would like to encrypt your report, say so in your first message
and we will arrange a secure channel or share a public key.

### 2. GitHub Private Security Advisory

Open a private report on the affected repository:

1. Go to the repository's **Security** tab.
2. Click **Report a vulnerability**.
3. Fill in the form. Only the repository's security maintainers will
   see the report.

GitHub's documentation for the [private vulnerability reporting
flow][privately-reporting] walks through the same steps with
screenshots.

## What to Include

A good report lets us reproduce the issue and assess impact quickly.
Please include as many of the following as you can:

- A descriptive title.
- The repository, package, version, and commit SHA affected.
- A clear description of the vulnerability and its impact.
- Steps to reproduce, ideally with a minimal proof of concept.
- Any logs, screenshots, or traffic captures that help.
- Your suggested remediation, if you have one.
- Whether you would like to be credited in the advisory, and how.

## Our Commitments

When you report a vulnerability in good faith, we commit to:

- Acknowledging receipt within **3 business days**.
- Providing an initial assessment (confirmed / not reproducible / out
  of scope / needs more information) within **10 business days**.
- Keeping you informed about remediation progress until the issue is
  resolved.
- Coordinating the disclosure timeline with you and crediting you in
  the published advisory unless you ask us not to.
- Not pursuing legal action against researchers who follow this policy
  in good faith (see **Safe Harbor** below).

## Scope

### In scope

- Any repository owned by [@nyuchi](https://github.com/nyuchi)
  unless explicitly marked as archived, experimental, or out of scope
  in its README.
- Published packages, container images, and releases produced by those
  repositories.
- Build and release infrastructure controlled by the organization
  (GitHub Actions workflows, release artifacts).
- Production services at `nyuchi.com`, `mukoko.com`, `siafudb.org`,
  `travel-info.co.zw`, `barstool.co.zw`, and related subdomains.

### Out of scope

- Vulnerabilities in third-party dependencies — please report those to
  the upstream project. If a dependency issue has a concrete impact on
  one of our projects, we do want to hear about _that_ impact.
- Issues on github.com itself or on hosting providers — report those
  directly to the relevant vendor
  (e.g., [GitHub's bug bounty][gh-bugbounty]).
- Social engineering, physical attacks, or denial-of-service attacks
  that rely on resource exhaustion alone.
- Reports generated solely by automated scanners with no demonstrated
  impact.

## Safe Harbor

We will not initiate or support legal action against you for security
research conducted in good faith against in-scope assets, provided that
you:

- Make a good-faith effort to avoid privacy violations, data
  destruction, service disruption, and degradation of user experience.
- Only interact with accounts you own or have explicit permission to
  access.
- Do not exfiltrate data beyond what is necessary to demonstrate the
  vulnerability, and delete any such data as soon as the report is
  acknowledged.
- Report the vulnerability privately through one of the channels
  above, and give us a reasonable window to remediate before any
  public disclosure.

This policy is not a waiver of rights against third parties and does
not authorize activity that would violate applicable law.

## Coordinated Disclosure

We prefer coordinated disclosure. Our default target is to publish a
fix and a GitHub Security Advisory within **90 days** of confirming a
vulnerability, or sooner for critical issues. If we need longer, we
will tell you and explain why.

Once a fix is released, we will credit the reporter by name and/or
handle in the advisory, unless the reporter requests otherwise.

## Thank You

Security research is a gift to our users. Thank you for taking the
time to report responsibly.

[privately-reporting]: https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing-information-about-vulnerabilities/privately-reporting-a-security-vulnerability
[gh-bugbounty]: https://bounty.github.com/
