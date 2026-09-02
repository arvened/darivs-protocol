
# DARIVS PROTOCOL

**Open standard for volunteer & charitable impact verification**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/)
[![JavaScript/TypeScript](https://img.shields.io/badge/JavaScript-ES2020%2B-yellow)](https://www.javascript.com/)

---
## ⚠️ Development Status

This repository is currently a **pre-grant proof-of-concept**. Development began ahead of the official NLnet grant execution period (September 1, 2026 – August 2027, Grant ID: 2026-06-4e7).

The existing schemas, specification, and examples demonstrate the protocol's viability and initial design. Grant funding will finance the **production-ready implementation**: JSON-LD parser & validator, Python/JavaScript SDKs, 60%+ test coverage, security audit, and community adoption.

See [docs/Status.md](docs/Status.md) for current development status.

---


## 📌 О ПРОЕКТЕ

**DARIVS PROTOCOL** — это открытый стандарт на базе JSON-LD для верификации волонтёрской деятельности и благотворительного воздействия. Протокол позволяет платформам обмениваться данными о добровольцах, проектах и влиянии де факто стандартизированным способом.

ЗАЧЕМ ЭТО НУЖНО
## 🔍 Чем отличается от существующих стандартов

| Стандарт | Что покрывает | Чего не хватает для DARIVS |
|---|---|---|
| schema.org (VolunteerAction) | Базовая разметка волонтёрской активности для поисковиков | Нет модели верификации, нет portable credentials, нет impact metrics |
| W3C Verifiable Credentials | Криптографическая верификация утверждений | Не специализирован под волонтёрство/благотворительность, нужна отдельная онтология для impact-данных |
| ActivityStreams 2.0 | Модель социальных действий (посты, лайки) | Не покрывает верификацию организаций и impact/hours tracking |

DARIVS PROTOCOL объединяет специфичную для volunteer/charity-домена онтологию (Organization, Volunteer, Activity, impact_metric) со встроенной моделью верификации — то, что в существующих стандартах разбросано по разным несовместимым спецификациям.


## 🚀 БЫСТРЫЙ СТАРТ

### Установка Python SDK

```bash
pip install darivs-protocol
```

### Пример 1: Создание записи о волонтёрской деятельности

```python
from darivs_protocol import VolunteerActivity, Organization

# Организация
org = Organization(
    id="https://example.org/orgs/red-cross",
    name="Red Cross Ukraine",
    country="UA",
    verified=True
)

# Запись о деятельности
activity = VolunteerActivity(
    volunteer_id="https://example.org/volunteers/alice",
    organization=org,
    activity_type="emergency_relief",
    hours=8,
    impact_metric="families_helped",
    impact_value=5,
    date="2026-06-29"
)

# Экспорт в JSON-LD
json_ld = activity.to_jsonld()
print(json_ld)
```

### Пример 2: Верификация данных

```python
from darivs_protocol import VerificationService

verifier = VerificationService()
result = verifier.verify(json_ld_data)

if result.is_valid:
    print(f"✅ Verified by: {result.verified_by}")
else:
    print(f"❌ Invalid: {result.errors}")
```

### Пример 3: JavaScript интеграция

```javascript
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

## 📋 КОМПОНЕНТЫ

### 1. **JSON-LD Specification** (`/spec`)

Полная спецификация формата данных:
- Core entities (Organization, Volunteer, Activity)
- Verification model
- Impact metrics
- Extensibility points

📖 [Читать спецификацию](/docs/SPECIFICATION.md)

### 2. **Python SDK** (`/python`)

Полнофункциональный SDK для Python 3.10+:
- Pydantic v2 models
- Validation & serialization
- Verification service
- Examples & tutorials

```bash
cd python
pip install -e .
pytest  # Run tests
```

### 3. **JavaScript SDK** (`/javascript`)

TypeScript-first SDK для Node.js и браузера:
- Full type safety
- Async/await support
- Verification service
- Examples & integrations

```bash
cd javascript
npm install
npm test
```

---

## 📚 ДОКУМЕНТАЦИЯ

| Документ | Описание |
|----------|---------|
| [SPECIFICATION.md](/docs/SPECIFICATION.md) | JSON-LD спецификация v0.1 (draft) |
| [PROJECT_STRUCTURE.md](/PROJECT_STRUCTURE.md) | Структура проекта и roadmap |
| [SPRINT_1_REPORT.md](/SPRINT_1_REPORT.md) | Отчёт о первом спринте |
| [COMMIT_LOG.md](/COMMIT_LOG.md) | История коммитов |

---

## 🔧 ПРИМЕРЫ ИНТЕГРАЦИЙ

### 1. Discord Bot 🤖

Бот для регистрации волонтёрской деятельности в Discord:

```bash
python examples/discord_bot.py
```

### 2. Telegram Bot 📱

Интеграция с Telegram для верификации:

```bash
python examples/telegram_bot.py
```

### 3. REST API Adapter 🌐

REST API wrapper для использования протокола в веб-приложениях:

```bash
python examples/rest_api.py
# Сервер слушает http://localhost:8000
```

### 4. Jupyter Analysis Notebook 📊

Анализ данных волонтёрской деятельности:

```bash
jupyter notebook examples/analysis.ipynb
```

### 5. CLI Utility 💻

Командная строка для работы с DARIVS данными:

```bash
python examples/cli_tool.py verify activity.json
python examples/cli_tool.py export --format jsonld
```

---

## ✅ ТРЕБОВАНИЯ

### Python SDK

- Python 3.10+
- pydantic >= 2.0
- pytest (для тестов)
- black, flake8, mypy (для quality checks)

### JavaScript SDK

- Node.js 16+
- TypeScript 4.5+
- Jest (для тестов)
- ESLint, Prettier (для quality checks)

---

## 📊 СТАТУС ПРОЕКТА
Завершено:
- ✅ JSON-LD specification outline (draft v0.1)
- ✅ Schema design document
- ✅ Python SDK skeleton
- ✅ README + examples directory
- ✅ GitHub Actions CI/CD
- ✅ 15+ commits, 20%+ coverage, 5+ issues

В процессе (после одобрения гранта):
- 🔄 Full Python SDK implementation
- 🔄 Full JavaScript SDK implementation
- 🔄 Integration examples (Discord, Telegram, REST)
- 🔄 60%+ test coverage

Планируется:
- ⏳ Production release (v1.0)
- ⏳ Security audit
- ⏳ Community adoption


---

## 🛠️ РАЗРАБОТКА

### Клонирование репо

```bash
git clone https://github.com/arvened/darivs-protocol.git
cd darivs-protocol
```

### Запуск тестов

```bash
# Python
cd python && pytest -v --cov=darivs_protocol

# JavaScript
cd javascript && npm test
```

### Code quality

```bash
# Python
black . && flake8 . && mypy .

# JavaScript
npm run lint && npm run format
```

---

## 📝 LICENSE

MIT License — see [LICENSE](/LICENSE) file

Copyright (c) 2026 ARVEN Agency

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...

---

## 🤝 CONTRIBUTING

Мы приветствуем контрибьюции! Пожалуйста:

1. Fork репо
2. Создай feature branch (`git checkout -b feature/amazing-thing`)
3. Коммитируй изменения (`git commit -m 'Add amazing thing'`)
4. Push в branch (`git push origin feature/amazing-thing`)
5. Открой Pull Request

**Требования для PR:**

- ✅ Tests included (60%+ coverage)
- ✅ Documentation updated
- ✅ Code passes linting (black, flake8, mypy)
- ✅ Atomic commits with clear messages

---

## 📬 КОНТАКТЫ

- **GitHub Issues:** [github.com/arvened/darivs-protocol/issues](https://github.com/arvened/darivs-protocol/issues)
- **Discussions:** [GitHub Discussions](https://github.com/arvened/darivs-protocol/discussions)
- **Email:** hello@arvend.io

---

## 🎯 ROADMAP

**Q2 2026 (June - August):**
- ✅ Specification v0.1 - v1.0
- ✅ Python SDK alpha
- ✅ JavaScript SDK alpha
- ✅ 3+ integration examples

**Q3 2026 (September - November):**
- 🔄 Production releases (v1.0)
- 🔄 Security audit
- 🔄 Community adoption (2+ platforms)
- 🔄 API documentation finalized

**Q4 2026 - Q3 2027:**
- ⏳ Extended SDKs (Go, Rust, Ruby)
- ⏳ Governance model
- ⏳ Official registry
- ⏳ Conference presentations

---

**Made with ❤️ by ARVEN Agency for NLnet NGI Zero Commons Fund**

*DARIVS PROTOCOL — Empowering volunteer communities through open standarts.
