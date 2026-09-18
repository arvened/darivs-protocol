# Frequently Asked Questions

## What is DARIVS PROTOCOL?

DARIVS PROTOCOL is an open JSON-LD standard for representing volunteer activities, organizational profiles, tasks, events, and impact metrics. It lets different volunteer and charity platforms exchange data about people, organizations, and their contributions in a common, interoperable format.

## Why not just use schema.org?

schema.org's `VolunteerAction` type provides basic markup for search engines, but it has no model for verification, portable credentials, or structured impact metrics. DARIVS PROTOCOL extends this idea with a domain-specific ontology (Volunteer, Organization, Task, Event, ImpactMetric) and a built-in verification model.

## Why not W3C Verifiable Credentials directly?

Verifiable Credentials provide the cryptographic verification layer, but they are domain-agnostic — you still need a specific data model for what's being verified. DARIVS PROTOCOL defines that data model for the volunteer/charity domain and is designed to be compatible with VC-based verification in future versions.

## Is this production-ready?

Not yet. The current repository is a **pre-grant proof-of-concept**: the JSON-LD schemas, specification, and examples are complete and stable, but the parser, validator, and SDKs are still in development. See [docs/Status.md](Status.md) for current progress.

## Can I use this in my platform today?

The schemas and specification are usable today for prototyping and integration planning. For production use, we recommend waiting for the v0.1.0 release, which will include a tested parser/validator and 60%+ test coverage.

## How can I contribute?

The repository is public under MIT license at [github.com/arvened/darivs-protocol](https://github.com/arvened/darivs-protocol). Issues and pull requests are welcome — see the specification in `docs/SPECIFICATION.md` for the current entity model.

## Who funds this project?

Development is supported by NLnet Foundation through the NGI Zero Commons Fund (Grant ID: 2026-06-4e7).

---

Have a question not answered here? Open an issue on GitHub.
