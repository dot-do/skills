# Security Policy

## Supported Versions

| Version | Supported |
|---------|-----------|
| latest (main) | ✅ |

## Reporting a Vulnerability

**Please do not report security vulnerabilities through public GitHub issues.**

If you discover a security vulnerability in this repository, please report it via email to **security@dot.do**.

Include:
- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Suggested fix (if any)

You will receive a response within 48 hours. We will work with you to understand and remediate the issue before any public disclosure.

## Scope

This repository contains markdown skill files for Claude Code agents. Security concerns may include:

- Skills that could lead to prompt injection
- Skills that expose sensitive patterns or credentials
- Skills that could enable unintended agent behaviors

## Out of Scope

- Vulnerabilities in Claude Code itself (report to Anthropic)
- Vulnerabilities in the `npx skills` toolchain (report to that project)
