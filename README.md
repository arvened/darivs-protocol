
# DARIVS PROTOCOL

**Open standard for volunteer & charitable impact verification**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/)
[![JavaScript/TypeScript](https://img.shields.io/badge/JavaScript-ES2020%2B-yellow)](https://www.javascript.com/)

---

## 📋 Development Status

This repository is currently a **pre-grant proof-of-concept**. Development began ahead of the official NLnet grant execution period (September 1, 2026 – August 2027, Grant ID: 2026-06-4e7).

The existing schemas, specification draft, and JSON-LD examples demonstrate the protocol's viability and initial design. **If funded**, grant funding will finance the production-ready implementation: a working JSON-LD parser & validator, Python/JavaScript SDKs, 60%+ test coverage, security audit, and community adoption.

**Nothing in this repository is published or installable yet.** The commands below describe the planned developer experience once SDKs are implemented.

See [docs/Status.md](docs/Status.md) for current development status.

---

## 🎯 What is DARIVS Protocol?

**DARIVS PROTOCOL** is a proposed open, JSON-LD-based data exchange format for verifying volunteer and charitable impact. The protocol aims to let platforms exchange data about volunteers, projects, and impact in a de facto standardized way.

## 📐 Schema Overview

| Entity | Based on | Notes |
|--------|----------|-------|
| schema.org (VolunteerAction) | Extends existing vocabulary with portable credentials, impact metrics |
| W3C Verifiable Credentials | Verification model |
| ActivityStreams 2.0 | Activity events (create, complete) |

DARIVS PROTOCOL defines JSON-LD schemas for volunteer/charity-adjacent core entities (Organization, Volunteer, Activity, impact_metric). The schemas currently exist as drafts; a reference implementation for validating and generating this data has not yet been built.

## 🚧 Planned Usage (not yet implemented)

### Python SDK (planned)

```bash
# Not yet published — will be available once the Python SDK is implemented
pip install darivs-protocol
```

```python
# Illustrative example of the planned API — this code does not run yet
from darivs_protocol import VolunteerActivity, Organization

org = Organization(
    id="https://example.org/orgs/red-cross",
    name="Red Cross Ukraine",
    country="UA",
    verified=True
)

activity = VolunteerActivity(
    volunteer_id="https://example.org/volunteers/alice",
    organization=org,
    activity_type="emergency_relief",
    hours=8,
    impact_metric="families_helped",
    impact_value=5,
    date="2026-06-29"
)

json_ld = activity.to_jsonld()
print(json_ld)
```

```python
# Illustrative example of the planned verification API — not yet implemented
from darivs_protocol import VerificationService

verifier = VerificationService()
result = verifier.verify(json_ld_data)

if result.is_valid:
    print(f"Verified by: {result.verified_by}")
else:
    print(f"Invalid: {result.errors}")
```

### JavaScript SDK (planned)

```javascript
// Illustrative example of the planned API — this code does not run yet
import { VolunteerActivity, Organization } from 'darivs-protocol';

const org = new Organization({
  id: 'https://example.org/orgs/unicef',
  name: 'UNICEF',
  country: 'UA'
});

const activity = new VolunteerActivity({
  volunteerId: 'https://example.org/volunteers/bob',
  organization: org,
  activityType: 'education',
  hours: 10
});

const jsonLd = activity.toJSONLD();
console.log(jsonLd);
```

---

## 📚 Components

### 1. JSON-LD Specification (`/schema`)

Contains the draft schema definitions for core entities:
- Core entities (Organization, Volunteer, Activity)
- Verification model
- Impact metrics
- Extensibility points

See [Specification draft](docs/SPECIFICATION.md).

### 2. Python SDK (`/python`) — not yet implemented

Planned SDK for Python 3.10+:
- Pydantic v2 models
- Validation & serialization
- Verification service
- Examples & tutorials

### 3. JavaScript SDK (`/javascript`) — not yet implemented

Planned TypeScript-first SDK for Node.js:
- Full type safety
- Async/await support
- Verification service
- Examples & integrations

---

## 📄 Documentation

| Document | Description |
|----------|-------------|
| [SPECIFICATION.md](docs/SPECIFICATION.md) | JSON-LD specification draft (v0.1 draft) |
| [PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md) | Repository layout and roadmap |
| [Status.md](docs/Status.md) | Current development status |
| [FAQ.md](docs/FAQ.md) | Frequently asked questions |

---

## 🔌 Planned Integrations (not yet implemented)

The `examples/` directory currently contains JSON-LD data examples only (no executable code yet). Once the SDKs exist, planned integration examples include a Discord bot, a Telegram bot, a REST API adapter, a Jupyter analysis notebook, and a CLI utility.

---

## 🛠 Tech Stack (planned)

### Python SDK
- Python 3.10+
- pydantic >= 2.0
- pytest (for tests)
- black, flake8, mypy (for quality checks)

### JavaScript SDK
- Node.js 16+
- TypeScript 4.5+
- Jest (for tests)
- ESLint, Prettier (for quality checks)

---

## ✅ Current Progress

What exists today:
- JSON-LD specification outline (draft v0.1)
- Schema design document
- README + examples directory (data examples only)
- GitHub Actions CI (validates existing JSON/JSON-LD files and required docs)

What remains to be built (if funded):
- Full Python SDK implementation
- Full JavaScript SDK implementation
- Integration examples (Discord, Telegram, REST)
- 60%+ test coverage
- Independent security audit
- Production release (v1.0)
- Community adoption

---

## 🚀 Getting Started (once implementation exists)

### Clone the repository

```bash
git clone https://github.com/arvened/darivs-protocol.git
cd darivs-protocol
```

### Running tests (once SDKs are implemented)

```bash
# Python
cd python && pytest -v --cov=darivs_protocol

# JavaScript
cd javascript && npm test
```

### Code quality (once SDKs are implemented)

```bash
# Python
black . && flake8 . && mypy .

# JavaScript
npm run lint && npm run format
```

---

## 📜 LICENSE

MIT License — see [LICENSE](/LICENSE) file

Copyright (c) 2026 ARVEN Agency

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...

---

## 🤝 CONTRIBUTING

We welcome contributions! Suggested workflow:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-thing`)
3. Commit your changes (`git commit -m 'Add amazing thing'`)
4. Push to the branch (`git push origin feature/amazing-thing`)
5. Open a Pull Request

**When opening a PR:**
'@
Set-Content -Path README.md -Value $readme -NoNewline
Get-Content README.md -TotalCount 10
```
