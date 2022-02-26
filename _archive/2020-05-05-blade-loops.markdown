---
layout: post
title: "Blade Loops"
categories: [programming, web-development]
---

Loops in Blade work same as in PHP.


# @for, @foreach, and @while


```
@for( $i = 0; $i < $talk->slotsCount(); $i++)
The number is {% raw %} {{ $i }} <br> {% endraw %}
@endfor
```

The `@foreach` and `@forelase` directives also provide `$loop` variable that returns `stdClass` object with following properties:
- index
- iteration
- remaining
- count
- first
- last
- depth
- parent

```
{% raw %}
<ul>
@foreach ($pages as $page)
<li> {{ $loop->iteration }}: {{$page->title}}
@if($page->hasChildren())
<ul>
@foreach ($page->children() as $child)
<li>{{ $loop->parent->iteration}}.
{{$loop->iteration }}:
{{ $child->title }}</li>
@endforeach
</ul>
@endif
</li>
@endforeach
</ul>
{% endraw %}
```


# The isSet() equivalent
```
{% raw %}

{{ $title or "Default" }}

{% endraw %}
```
This echoes either value of {% raw %}`$title`{% endraw %} or `"Default"`.





> Excerpts from the book `Laravel: Up and Running by Matt Stauffer`
