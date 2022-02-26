---
layout: post
title: "Blade Template Inheritence"
categories: [programming, web-development]
---

Blade template allows single inheritence

# @section @endsection/@show, @yield and @content

`@section @endsection/@show @yield and @content` directives can be used to inherit templates. 

## `@content('title')` and `@yield('title')`
These directives allow **title** to be displayed by the child view. Otherwise nothing will be shown.

## `@content('title','Homepage')` and `@yidle('title','Homepage')`
These directives are same as with a single parameters, only difference is the latter parameters are used as default if the subclassing child does not display the **title**.

## `@section('page')...@show`
This directive allows place of the content to be defined by a parent view. The `@section('page')...@show` directives are used in the parent view, e.g in a generic wrapper view.


## `@section('page')...@endsection`
This directive allows part of the content to be displayed in a child. The `@section('page')...@endsection` directives are used in the child view.



> Excerpts from the book `Laravel: Up and Running by Matt Stauffer`
