---
layout: post
title: "TensorFlow on MacOS"
date: '2018-11-26T03:06:44Z'
comments: true
categories: [tensorflow]
published: true
---

I was very excited to start running TensorFlow Python programs on my Mac.

I installed it using PIP, using the instructions provided by [TensorFlow.org](https://www.tensorflow.org/). On running my first TensorFlow program, the first thing it output was:

```
2018-11-25 19:13:07.524017: I tensorflow/core/platform/cpu_feature_guard.cc:141] Your CPU supports instructions that this TensorFlow binary was not compiled to use: SSE4.1 SSE4.2 AVX AVX2 FMA
```

This didn't look good, it turned out it's just a warning. My program worked, but wasn't running
as fast as it could. I don't want to be hobbled by an inferior version of TensorFlow. I want the
optimized version!

After some investigation, the way to resolve the warning is to compile TensorFlow from source:

https://www.tensorflow.org/install/source

When installing from source, the installer will prompt you for options. To keep things simple and maximize
the chance of success, use the default values provided.
