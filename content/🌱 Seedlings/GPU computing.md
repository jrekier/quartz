---
tags:
  - 🖥️Computing
  - 🖍️Learning
---
CPU excel at doing complex computations serially.
GPU can only do simple computations, but there are typically many of them. 

This is simple enough and gets repeated abundantly on the internet. However it’s never really clear what exactly causes that.

One of the main reason is that distributing small tasks across many GPU cores is a complex task handled by the CPU. 

This [stackexchange answer](https://scicomp.stackexchange.com/a/25151/19584) is particularly enlightening. Excerpt:
>[!quote]
>Linear algebra is one domain where parallelism is really well established. Thus the best way to write for a GPU is to essentially have the GPU do all of the linear algebra: it essentially becomes a card to compute `Ax=b` and `A*B` much faster than the CPU [...]. ==But there's a caveat: data transfer to GPUs is really slow. Also, memory allocation on GPUs is really slow.==
>So while the linear algebra is fast, you have to deal with the fact that:
>1. Serial performance is awful.
>2. Allocating memory dynamically on the GPU destroys performance.
>3. Transferring back and forth between the CPU and GPU is slow.
>
>This puts constraints on your algorithm: you need to try to leave as much on the GPU as possible, transferring back and forth the minimum amount, while trying to avoid serial parts from running on the GPU.

