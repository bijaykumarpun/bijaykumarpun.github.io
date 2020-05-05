---
layout: post
title: "Blade Control Structures"
categories: [programming, web-development]
---

> Excerpts from the book `Laravel: Up and Running by Matt Stauffer`

Control structures in Blade look cleaner than in plain PHP. Some examples below:

```
@if( cocunt($talks) === 1)
There is one talk at this time period.
@elseif (count($talks===0)
There are no talks at this time period.
@else
There are {{ count($talks) }} at this time period.
@endif
```

Blade's `@if ($condition)` is as `<? php if ($condition): ?>` in PHP. So is for `@else`, `@elseif`, and `@endif`.


# @unless and @endunless

`@unless` is the direct inverse of `@if`, and has no equivalent code in PHP. `@unless ($condition)` is the same as `<?php if (!$condition) ?>`.


```
@unless ($user ->hasPaid())
You can complete your payment by switching to the payment tab.
@endunless
```
