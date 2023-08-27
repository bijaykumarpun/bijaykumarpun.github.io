---
layout: post
title: "Clean Architecture Pattern"
date: 2023-06-24 18:00:00
description: "Design pattern"
---

---
#### Principles

- Separation of concerns
- Drive UI from data models
- Single source of truth
- Unidirectional data flow (States & events flow in opposite directions)

#### Modules

```
app
domain (optional)
data
```

#### Data flow

<img src="/assets/img/posts/clean-architecture-dfd.png" width="700"/>

#### Example folder structure

```
// Android project

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
