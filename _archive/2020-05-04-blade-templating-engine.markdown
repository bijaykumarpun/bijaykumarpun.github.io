---
layout: post
title: "Laravel's Blade Templating Engine"
categories: [programming, web-development]
---

> Excerpts from the book `Laravel: Up and Running by Matt Stauffer`

Laravel's Blade templating engine is inspired from .NET's [Razor](https://en.wikipedia.org/wiki/ASP.NET_Razor) engine. It supports inheritence and extensibility.

```
{!! $group->heroImageHtml() !!}

@forelse ($users as $user)
{{$user->first_name }} {{ $user->last_name }}<br>
@empty
No users in this group.
@endforelse
```

The custom tags are called `directives` and are prefixed with `@`. All Blade syntax is compiled into normal PHP code and cached, and also allows to use native PHP in Blade files, though not recommended.

## Echoing data
To echo data, just use {% raw %} `{{ $variable  }}` {% endraw %}. It is similar to {% raw %} `<?= $variable ?>` {% endraw %} in plain PHP. Also,  Blade escapes all echoes by default using `htmlentities()`, which means  {% raw %} `{{ $variable}}` {% endraw %} is equivalent to `<?= htmlentities($variable) ?>`. In order to echo without escaping, `{!! !!}` can be used.


