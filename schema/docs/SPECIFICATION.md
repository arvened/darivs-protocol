
# 📝 FILE 8: `docs/SPECIFICATION.md`

**Путь:** `docs/SPECIFICATION.md`

Это **БОЛЬШОЙ файл** (25+ страниц). Скопируй **весь текст:**

# 📄 Скопируй весь этот текст:

```markdown
# DARIVS PROTOCOL Specification v0.1.0

**Status:** Draft (Alpha)  
**Version:** 0.1.0-alpha  
**Date:** June 29, 2026  
**Maintainer:** Eduard Arbitman, ARVEN Agency

---

## Table of Contents

1. [Overview](#overview)
2. [Core Entities](#core-entities)
3. [JSON-LD Context](#json-ld-context)
4. [Relationships](#relationships)
5. [Data Types & Formats](#data-types--formats)
6. [Validation Rules](#validation-rules)
7. [Examples](#examples)
8. [Extensibility](#extensibility)
9. [Versioning](#versioning)

---

## Overview

**DARIVS PROTOCOL** is an open standard for representing volunteer activities, organizational profiles, tasks, events, and impact metrics using JSON-LD (JSON for Linked Data).

### Design Principles

1. **Interoperability** — Enable data exchange between platforms
2. **Simplicity** — Easy to implement and use
3. **Extensibility** — Support custom properties and relationships
4. **Portability** — Volunteers can export their data
5. **Privacy** — Respect user privacy and GDPR compliance
6. **Verification** — Support impact verification and measurement

### Use Cases

- Volunteer platforms share volunteer profiles across ecosystems
- Organizations exchange task listings
- Communities track volunteer impact
- Platforms integrate volunteer data from multiple sources
- Volunteers maintain portable records of their contributions

---

## Core Entities

### 1. Volunteer

**Entity Type:** `Volunteer`  
**URI:** `https://darivs.protocol/schema/volunteer-v0.1.0`

Represents an individual volunteer with skills, availability, and participation history.

#### Required Properties

```json
{
  "id": "string (URI)",
  "type": "Volunteer",
  "firstName": "string",
  "lastName": "string",
  "email": "string (email)",
  "createdAt": "string (ISO 8601)"
}
```

#### Key Properties

| Property | Type | Description |
|----------|------|-------------|
| `id` | URI | Unique volunteer identifier (e.g., `https://platform.org/volunteers/alice-123`) |
| `type` | Enum | Always `"Volunteer"` |
| `firstName` | String | First name (1-100 chars) |
| `lastName` | String | Last name (1-100 chars) |
| `email` | Email | Contact email address |
| `avatar` | URI | Profile picture URL |
| `bio` | String | Short biography (max 500 chars) |
| `skills` | Array | Array of skills with proficiency levels |
| `languages` | Array | Languages spoken with proficiency |
| `availability` | Object | Hours per week, date range, recurring patterns |
| `location` | Object | Country, region, city, coordinates |
| `participates` | Array | References to Tasks and Events |
| `coordinates` | Array | References to Tasks coordinated |
| `socialMedia` | Object | Social media profile links |
| `preferences` | Object | Task preferences, remote/team size, impact focus |
| `verified` | Boolean | Profile verification status |

#### Example

```json
{
  "@context": "https://darivs.protocol/schema/darivs-context.jsonld",
  "id": "https://helpua.org/volunteers/alice-ua",
  "type": "Volunteer",
  "firstName": "Alice",
  "lastName": "Kovalenko",
  "email": "alice@example.ua",
  "avatar": "https://example.ua/avatars/alice.jpg",
  "bio": "Experienced teacher, fluent in English and Ukrainian",
  "skills": [
    {
      "skill": "Teaching",
      "skillLevel": "expert",
      "yearsOfExperience": 8
    },
    {
      "skill": "English Translation",
      "skillLevel": "advanced",
      "yearsOfExperience": 5
    }
  ],
  "languages": [
    {
      "language": "uk",
      "proficiency": "native"
    },
    {
      "language": "en",
      "proficiency": "fluent"
    }
  ],
  "availability": {
    "hoursPerWeek": 10,
    "startDate": "2026-06-01"
  },
  "location": {
    "country": "UA",
    "city": "Kyiv"
  },
  "createdAt": "2026-06-15T10:30:00Z",
  "verified": true
}
```

---

### 2. Organization

**Entity Type:** `Organization`  
**URI:** `https://darivs.protocol/schema/organization-v0.1.0`

Represents a nonprofit organization, charity, or institution.

#### Required Properties

```json
{
  "id": "string (URI)",
  "type": "Organization",
  "name": "string",
  "email": "string (email)",
  "country": "string",
  "createdAt": "string (ISO 8601)"
}
```

#### Key Properties

| Property | Type | Description |
|----------|------|-------------|
| `id` | URI | Unique organization identifier |
| `name` | String | Legal organization name |
| `shortName` | String | Acronym or short name |
| `description` | String | Detailed description (max 2000 chars) |
| `email` | Email | Contact email |
| `website` | URI | Organization website |
| `legalStatus` | Enum | `npo`, `ngo`, `charity`, `cooperative`, etc. |
| `registrationNumber` | String | Government registration (e.g., ЄДРПОУ) |
| `taxId` | String | Tax identification number |
| `country` | String | ISO 3166-1 alpha-2 country code |
| `location` | Object | Full address and coordinates |
| `founded` | Date | Organization founding date |
| `mission` | String | Mission statement |
| `focusAreas` | Array | Areas of focus (emergency, education, health, etc.) |
| `staffCount` | Integer | Number of paid staff |
| `volunteerCount` | Integer | Number of active volunteers |
| `coordinates` | Array | Coordinating volunteers |
| `organizes` | Array | Tasks and events organized |
| `verified` | Boolean | Verification status |

#### Example

```json
{
  "@context": "https://darivs.protocol/schema/darivs-context.jsonld",
  "id": "https://darivs.platform/orgs/red-cross-ua",
  "type": "Organization",
  "name": "Red Cross Ukraine",
  "shortName": "RCU",
  "email": "info@redcross.ua",
  "website": "https://redcross.ua",
  "country": "UA",
  "legalStatus": "npo",
  "registrationNumber": "ЄДРПОУ 12345678",
  "mission": "To provide humanitarian relief and support communities in crisis",
  "focusAreas": ["emergency_relief", "health", "social_services"],
  "staffCount": 50,
  "volunteerCount": 200,
  "location": {
    "country": "UA",
    "city": "Kyiv",
    "address": "123 Main Street"
  },
  "createdAt": "2026-01-01T00:00:00Z",
  "verified": true,
  "verificationMethod": "government_records"
}
```

---

### 3. Task

**Entity Type:** `Task`  
**URI:** `https://darivs.protocol/schema/task-v0.1.0`

Represents a volunteer task or project.

#### Required Properties

```json
{
  "id": "string (URI)",
  "type": "Task",
  "taskTitle": "string",
  "taskDescription": "string",
  "taskCreatedBy": "string (URI)",
  "createdAt": "string (ISO 8601)"
}
```

#### Key Properties

| Property | Type | Description |
|----------|------|-------------|
| `id` | URI | Unique task identifier |
| `taskTitle` | String | Task name (5-200 chars) |
| `taskDescription` | String | Detailed description (10-5000 chars) |
| `taskCategory` | Enum | emergency_response, education, mentoring, technical, etc. |
| `taskStatus` | Enum | open, in_progress, on_hold, completed, cancelled |
| `skillsRequired` | Array | Required skills with minimum levels |
| `hoursRequired` | Integer | Estimated total hours |
| `urgency` | Enum | low, medium, high, critical |
| `startDate` | Date | Task start date |
| `deadline` | Date | Task deadline |
| `location` | Object | Remote/onsite/hybrid + address |
| `taskCreatedBy` | URI | Creator (volunteer or organization) |
| `organization` | URI | Organization task belongs to |
| `participates` | Array | Participating volunteers |
| `maxVolunteers` | Integer | Maximum volunteers needed |
| `deliverables` | Array | Expected outcomes |
| `impactMetrics` | Array | How impact will be measured |
| `verified` | Boolean | Verification status |

#### Example

```json
{
  "@context": "https://darivs.protocol/schema/darivs-context.jsonld",
  "id": "https://helpua.org/tasks/english-tutoring-2026",
  "type": "Task",
  "taskTitle": "English Language Tutoring for Refugees",
  "taskDescription": "Help refugee families learn English for job interviews and daily life",
  "taskCategory": "education",
  "taskStatus": "open",
  "skillsRequired": [
    {
      "skill": "English",
      "minimumLevel": "advanced",
      "required": true
    },
    {
      "skill": "Teaching",
      "minimumLevel": "intermediate",
      "required": false
    }
  ],
  "hoursRequired": 40,
  "deadline": "2026-08-31",
  "location": {
    "remote": true,
    "onsite": false
  },
  "organization": "https://helpua.org/orgs/help-ukraine",
  "participates": [
    "https://helpua.org/volunteers/alice-ua",
    "https://helpua.org/volunteers/bob-us"
  ],
  "maxVolunteers": 5,
  "currentVolunteers": 2,
  "createdAt": "2026-06-20T14:30:00Z",
  "verified": true
}
```

---

### 4. Event

**Entity Type:** `Event`  
**URI:** `https://darivs.protocol/schema/event-v0.1.0`

Represents a volunteer event or gathering.

#### Required Properties

```json
{
  "id": "string (URI)",
  "type": "Event",
  "eventTitle": "string",
  "eventDescription": "string",
  "eventDate": "string (date)",
  "eventOrganizer": "string (URI)",
  "createdAt": "string (ISO 8601)"
}
```

#### Key Properties

| Property | Type | Description |
|----------|------|-------------|
| `id` | URI | Unique event identifier |
| `eventTitle` | String | Event name |
| `eventDescription` | String | Detailed description |
| `eventType` | Enum | volunteer_day, workshop, training, conference, etc. |
| `eventDate` | Date | Event start date |
| `eventTime` | Time | Event start time |
| `endDate` | Date | End date (for multi-day events) |
| `status` | Enum | planned, ongoing, completed, cancelled, postponed |
| `location` | Object | Venue, address, virtual/hybrid info |
| `eventOrganizer` | URI | Organizing organization or volunteer |
| `registrationRequired` | Boolean | Whether registration is required |
| `maxAttendees` | Integer | Venue capacity |
| `currentAttendees` | Integer | Current registrations |
| `participates` | Array | Attending volunteers |
| `agenda` | Array | Detailed schedule |
| `catering` | Object | Meal and refreshment info |
| `accessibility` | Object | Wheelchair access, interpreters, etc. |
| `verified` | Boolean | Verification status |

#### Example

```json
{
  "@context": "https://darivs.protocol/schema/darivs-context.jsonld",
  "id": "https://darivs.platform/events/cleanup-2026-july",
  "type": "Event",
  "eventTitle": "Community Cleanup Day - Kyiv",
  "eventDescription": "Join us for a community cleanup of local parks and streets",
  "eventType": "volunteer_day",
  "eventDate": "2026-07-15",
  "eventTime": "09:00",
  "eventOrganizer": "https://darivs.platform/orgs/green-kyiv",
  "location": {
    "city": "Kyiv",
    "country": "UA",
    "venue": "Central Park"
  },
  "maxAttendees": 100,
  "currentAttendees": 45,
  "registrationRequired": true,
  "accessibility": {
    "wheelchairAccessible": true,
    "parking": true
  },
  "createdAt": "2026-06-01T10:00:00Z",
  "verified": true
}
```

---

### 5. ImpactMetric

**Entity Type:** `ImpactMetric`  
**URI:** `https://darivs.protocol/schema/impact-v0.1.0`

Represents a measured or recorded impact of volunteer activity.

#### Required Properties

```json
{
  "id": "string (URI)",
  "type": "ImpactMetric",
  "impactType": "string (enum)",
  "impactValue": "number",
  "impactUnit": "string (enum)",
  "recordedBy": "string (URI)",
  "impactDate": "string (date)",
  "createdAt": "string (ISO 8601)"
}
```

#### Key Properties

| Property | Type | Description |
|----------|------|-------------|
| `id` | URI | Unique impact record identifier |
| `impactType` | Enum | lives_helped, families_assisted, people_trained, etc. |
| `impactValue` | Number | Numeric value |
| `impactUnit` | Enum | people, families, hours, kg, items, currency, etc. |
| `description` | String | Detailed description |
| `impactDate` | Date | Date impact occurred |
| `volunteer` | URI | Volunteer who generated impact |
| `organization` | URI | Organization (beneficiary or coordinator) |
| `task` | URI | Related task |
| `event` | URI | Related event |
| `recordedBy` | URI | Who recorded the impact |
| `verifiedBy` | URI | Who verified it |
| `verificationMethod` | Enum | self_reported, coordinator_confirmed, third_party_audit, etc. |
| `evidenceLinks` | Array | Links to photos, documents, certificates |
| `beneficiaries` | Array | Who benefited |
| `sdgAlignment` | Array | UN SDG numbers (1-17) |
| `verified` | Boolean | Verification status |

#### Example

```json
{
  "@context": "https://darivs.protocol/schema/darivs-context.jsonld",
  "id": "https://darivs.platform/impact/2026-june-tutoring-alice",
  "type": "ImpactMetric",
  "impactType": "people_trained",
  "impactValue": 15,
  "impactUnit": "people",
  "description": "English language training provided to refugee families",
  "impactDate": "2026-06-30",
  "volunteer": "https://helpua.org/volunteers/alice-ua",
  "task": "https://helpua.org/tasks/english-tutoring-2026",
  "recordedBy": "https://helpua.org/volunteers/alice-ua",
  "verifiedBy": "https://helpua.org/orgs/help-ukraine",
  "verificationMethod": "coordinator_confirmed",
  "beneficiaries": [
    {
      "type": "family",
      "count": 5
    }
  ],
  "sdgAlignment": [4, 10],
  "createdAt": "2026-06-30T18:00:00Z",
  "verified": true
}
```

---

## JSON-LD Context

The DARIVS Protocol uses a JSON-LD context to map property names to URIs and define data types.

### Context URL

```
https://darivs.protocol/schema/darivs-context.jsonld
```

### Using the Context

All DARIVS Protocol documents should reference the context:

```json
{
  "@context": "https://darivs.protocol/schema/darivs-context.jsonld",
  "id": "https://example.org/volunteers/alice",
  "type": "Volunteer",
  ...
}
```

### Key Namespace Mappings

| Prefix | Namespace |
|--------|-----------|
| `darivs` | `https://darivs.protocol/ontology/` |
| `schema` | `https://schema.org/` |
| `rdf` | `http://www.w3.org/1999/02/22-rdf-syntax-ns#` |
| `xsd` | `http://www.w3.org/2001/XMLSchema#` |

---

## Relationships

DARIVS Protocol defines key relationships between entities:

### Participation Relationships

- **Volunteer participates in Task** (many-to-many)
- **Volunteer participates in Event** (many-to-many)

### Coordination Relationships

- **Volunteer coordinates Task** (one-to-many)
- **Organization organizes Task** (one-to-many)
- **Organization organizes Event** (one-to-many)

### Involvement Relationships

- **Organization involves Volunteer** (one-to-many)

### Impact Relationships

- **Volunteer generates ImpactMetric** (one-to-many)
- **Task generates ImpactMetric** (one-to-many)
- **Event generates ImpactMetric** (one-to-many)

### Relationship Example

```json
{
  "id": "https://helpua.org/volunteers/alice",
  "type": "Volunteer",
  "participates": [
    "https://helpua.org/tasks/english-tutoring-2026",
    "https://helpua.org/events/cleanup-2026-july"
  ],
  "coordinates": [
    "https://helpua.org/tasks/mentoring-program"
  ]
}
```

---

## Data Types & Formats

### Date & Time Formats

- **Date:** ISO 8601 `YYYY-MM-DD` (e.g., `2026-06-15`)
- **Time:** ISO 8601 `HH:MM` or `HH:MM:SS` (e.g., `14:30:00`)
- **DateTime:** ISO 8601 with timezone (e.g., `2026-06-15T14:30:00Z`)

### URI Format

Identifiers must be valid URIs:
```
https://platform.org/volunteers/alice-123
https://platform.org/organizations/red-cross-ua
https://platform.org/tasks/emergency-response-2026
```

### Email Format

Must be valid email address:
```
alice@example.ua
info@redcross.ua
```

### Enumerations

All enum properties must use exact values from schema.

---

## Validation Rules

### Entity-Specific Rules

#### Volunteer
- `firstName` and `lastName` cannot be empty
- `email` must be valid email format
- `skills` array can have multiple skills
- `availability.hoursPerWeek` must be 0-168

#### Organization
- `name` is required and cannot be empty
- `country` must be valid ISO 3166-1 alpha-2 code
- `registrationNumber` format depends on country

#### Task
- `taskTitle` must be 5-200 characters
- `deadline` must be after `startDate`
- `hoursRequired` must be positive integer
- `maxVolunteers` >= `currentVolunteers`

#### Event
- `eventDate` cannot be in past
- `eventTime` format must be valid
- `maxAttendees` >= `currentAttendees`

#### ImpactMetric
- `impactValue` must be non-negative
- `impactDate` <= `createdAt`
- `verified` can only be true if `verifiedBy` is set

### Cross-Entity Rules

- All entity IDs must be unique within their namespace
- Foreign key references (URIs) should be valid
- Timestamps must be in ISO 8601 format

---

## Examples

### Complete Volunteer Profile

[See Volunteer section for full example]

### Complete Organization Profile

[See Organization section for full example]

### Task with Multiple Volunteers

[See Task section for full example]

### Event with Full Details

[See Event section for full example]

### Impact Record with Evidence

[See ImpactMetric section for full example]

---

## Extensibility

### Custom Properties

The DARIVS Protocol can be extended with custom properties:

```json
{
  "@context": [
    "https://darivs.protocol/schema/darivs-context.jsonld",
    {
      "customField": "https://custom.namespace/customField"
    }
  ],
  "id": "https://example.org/volunteers/alice",
  "type": "Volunteer",
  "firstName": "Alice",
  "customField": "Custom Value"
}
```

### Custom Entity Types

New entity types can be defined following the same pattern as core entities:

```json
{
  "@context": "https://darivs.protocol/schema/darivs-context.jsonld",
  "id": "https://example.org/projects/climate-action",
  "type": "Project",
  "projectName": "Climate Action Initiative",
  ...
}
```

---

## Versioning

### Version Numbering

DARIVS Protocol follows Semantic Versioning:
- **Major version** (v1, v2, ...) — Breaking changes
- **Minor version** (.1, .2, ...) — New features, backwards compatible
- **Patch version** (.0.1, .0.2, ...) — Bug fixes

### Current Version

**0.1.0-alpha** (Draft, under development)

### Planned Versions

- **0.1.0** (Production) — Q3 2026
- **0.2.0** — Q4 2026 (Cryptographic signing)
- **1.0.0** — Q2 2027 (Formal specification)

---

## References

- [JSON-LD Specification](https://www.w3.org/TR/json-ld11/)
- [JSON Schema](https://json-schema.org/)
- [Schema.org](https://schema.org/)
- [UN Sustainable Development Goals](https://sdgs.un.org/)

---

**DARIVS PROTOCOL — Open Standard for Volunteer Impact Verification**

*Maintained by Eduard Arbitman, ARVEN Agency*  
*Funded by NLnet Foundation — NGI Zero Commons Fund*
```

---

## 📋 ИНСТРУКЦИЯ:

1. **"Add file"** → **"Create new file"**
2. **"Name":** `docs/SPECIFICATION.md`
3. Скопируй **весь текст выше** (692 строки)
4. Paste в текстовое поле
5. **"Commit changes"** → Сообщение: `docs: add full JSON-LD specification v0.1.0`
6. **"Commit"**

---

✅ **Файл 8 готов! (Самый большой файл)**

Загружай → пиши "Да" → дам файлы 9-13 (остальные docs + примеры) 👉




