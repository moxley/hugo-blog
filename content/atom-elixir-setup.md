---
layout: post
title: "Atom Editor Setup for Elixir"
date: '2018-10-06 10:02:41 -0700'
comments: true
categories: ['elixir', 'atom']
published: true
---
When working with Elixir, I want the following support from my editor:

- Elixir syntax highlighting
- Compiler errors and warnings displayed while I'm editing Elixir code
- Automatic Elixir code formatting
- Automatic [Dialyzer](http://hex.pm/packages/dialyxer) checking and reporting when I save an Elixir code file

These are the following plugins that provide those features:

- `language-elixir`
- `ide-elixir`
- `atom-elixir-formatter`
- `linter-elixir-credo`

Before installing any of these packages, read their README pages carefully.

## language-elixir

https://atom.io/packages/language-elixir

This is the minimal package you want to use when developing Elixir code.
It provides code syntax highlighting.

## ide-elixir

https://atom.io/packages/ide-elixir

The most value I get out of IDE Elixir is the feedback it gives from the Elixir
compiler, and from [Dialyzer](http://hex.pm/packages/dialyxer).

If you don't care so much about the Dialyzer support, and you want something
more lightweight, I recommend <a
href="https://atom.io/packages/linter-elixirc">`linter-elixirc`</a>.

## atom-elixir-formatter

https://atom.io/packages/atom-elixir-formatter

This package formats Elixir code with the Elixir Formatter, which is built into
Elixir 1.6 and up. One side utility of this package is that it allows you to
paste in large data structures from test output into your test or fixtures, then
easily format the resulting code.

## linter-elixir-credo

https://atom.io/packages/linter-elixir-credo

This package integrates with Credo to report into code style and consistency.
