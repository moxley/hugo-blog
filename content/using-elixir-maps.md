---
layout: post
title: "Using Elixir Maps"
date: '2018-10-13T18:38:56Z'
comments: true
categories: ['elixir']
published: false
---
A little background on the way I see string key maps versus atom keys... We tend to compose an application's design into layers, kind of like an onion. The top layers are where the input comes in, and the inner layers are the pure, essential application logic. Data flows from the outer layers to the inner, then back out again. The data in the outer layers tends to be messy, unparsed, unrefined. For maps, that would be string keys. As the data flows to the inner layers, it gets parsed and refined. Maps with string keys become maps with atom keys, preferably with a know set of keys (aka structs).

This `Recipients` module is one of the inner layers of the application. Seeing it take a map with string keys is a sign that the data hasn't been parsed sufficiently.

Defining a core module that accepts string keys implies you’ve implemented in a top-down approach.
