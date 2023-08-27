---
layout: post
title: "Clean architecture pattern"
date: 2023-06-24 18:00:00
description: "Design pattern"
---

---
### Module separation

```
app
domain (optional)
data
```

### Properties

- Independent of framework
- Testable
- Independent of UI
- Independent of database
- Independent of any external agency

### Data flow

<img src="/assets/img/al-folio-preview.png>

### Example project folder structure

> Android project

```
  ├── MyWeatherApplication.kt
├── data
│   ├── repositories
│   └── source
│       ├── device
│       └── weather
├── domain
│   ├── models
│   └── use_cases
│       ├── device
│       └── weather
├── infrastructure
│   └── di
└── presentation
    ├── framework
    │   └── theme
    └── screen
        ├── home
        │   └── model
        ├── settings
        └── weather_detail
```
---
