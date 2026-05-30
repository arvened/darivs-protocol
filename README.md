
# Darivs Protocol

> Open Standard for Community Engagement Platforms

Good Just Happens.

-----

## What is Darivs Protocol?

Darivs Protocol is an open standard that defines how community engagement and charitable giving platforms should work — transparently, verifiably, and without vendor lock-in.

Any NGO, foundation, or civic organization can deploy a platform based on this protocol where collective action creates social good automatically.

-----

## The Problem

Existing charitable platforms are proprietary and fragmented:

- No interoperability between platforms
- Communities have no sovereignty over their infrastructure
- Cross-jurisdiction operation (EU + UA) requires separate systems
- Every organization must build from scratch or accept vendor dependency

-----

## The Solution

The Darivs Protocol specifies:

- Challenge lifecycle — creation → validation → completion → reward distribution
- Donation flows — transparent multi-party splits with verifiable audit trails
- Community governance — how communities fork and self-govern their instance
- Cross-jurisdiction support — EU (Stripe/SEPA) + UA (LiqPay) with GDPR by design

### Split model

|Jurisdiction|Winner|Fund|Platform|
|------------|------|----|--------|
|EU (EUR)    |55%   |35% |10%     |
|UA (UAH)    |53%   |35% |12%     |

-----

## Five Directions

1. 🐾 Animal Protection — war-affected animals in Ukraine
1. 👶 Children — children’s welfare programs
1. 🌱 Ecology — environmental initiatives
1. 🤝 Civil Society — volunteers and civic participation
1. ✡️ Religious & Community Foundations — Jewish life, interfaith programs

-----

## Reference Implementation

The reference implementation is built on:

- Backend: Node.js + Fastify
- Frontend: Next.js 14
- Database: PostgreSQL + Prisma
- Queue: Redis + BullMQ
- Payments: Stripe Connect (EU) + LiqPay (UA)
- Realtime: Socket.io
- Infrastructure: Docker + Turborepo

Live platform: [darivs.com](https://darivs.com)

-----

## Proof of Concept

Core formula: weak + autonomous > smart + dependent

Validated by: *Zero Latency* — 68 chapters · 54 autonomous runs · 0 manual stops · built with Claude Code.

-----

## Partners

|Organization                   |Country  |Role                       |
|-------------------------------|---------|---------------------------|
|Charity Fund “Glory of Ukraine”|Ukraine 🇺🇦|Lead applicant, governance |
|TuS Makkabi Leichlingen e.V.   |Germany 🇩🇪|Community validation, pilot|
|Darivs OÜ                      |Estonia 🇪🇪|EU legal entity, IP holder |
|FOP Arbitman Eduard            |Ukraine 🇺🇦|Lead developer, architect  |

-----

## Status

|Milestone                     |Date       |Amount |Status   |
|------------------------------|-----------|-------|---------|
|MVP + Protocol Spec v1.0      |Dec 1, 2026|€10,500|🔜 Planned|
|Full platform + Security Audit|Apr 1, 2027|€14,000|🔜 Planned|
|Final release + Report        |Aug 1, 2027|€10,500|🔜 Planned|

Funded by: NGI Zero Commons Fund (NLnet Foundation) · €35,000 · 12 months

-----

## License

MIT License — see <LICENSE>

All protocol specifications, documentation, and reference implementation code are free and open source.

-----

## Contact

ARVEN AI Agency

- Web: [arvend.io](https://arvend.io)
- Email: [hello@arvend.io](mailto:hello@arvend.io)
- Telegram: [@arven_agency](https://t.me/arven_agency)

-----

*Good Just Happens.*
