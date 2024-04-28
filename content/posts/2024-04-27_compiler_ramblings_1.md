
+++
title = "Misadventures in Compiler Design - Part 1"
+++

Im writing a compiler, and Im learning very quickly about how little I know.
This post is lovingly titled *Part 1* because I have a feeling theres more where this came from.

<!-- more -->

---

Quick little introduction to the project:
- Im writing a compiler for a language I'm designing
- Written in Rust
- Handwritten LL(1) parser
- Cranelift for codegen

Preliminary syntax looks like this:

```rust
fn fib(n: i32): i32 = {
    let result: i32 = 0;
    if n <= 1 then {
        result = n;
    } else {
        result = fib(n - 1) + fib(n - 2);
    }
    return result;
}
```

And this code does actually run at this point in time.

---

I've been making a lot of progress over the last few weeks, and I would consider the current state of the project a good MVP, and now's the time to really hit the brakes and think about the correctness of the pipeline. I admit it's really quite wrong in a lot of ways.

The biggest issue is that It preforms no sort of AST validation or lowering.

Yes. I'm doing codegen directly from the loosely typed AST. This is usually how you'd do it in a toy language, or in a language with a much looser type system, but theres a couple reasons this is almost always a bad idea.

**- It forces you to handle typing in the codegen phase.**

This might be the most significant issue. If your language has any sort of type-system, it's gotta go somewhere. So if it's not its own step in the frontend section, you're just kicking the can down the road, and increasing the complexity of the codegen phase.

The way I have it right now, the code generation code is littered with type checks. Coercions don't exist right now, all types need to match up exactly, but if they did exist, let-alone any more complex level of inference, the codegen phase would be even more of a nightmare than it already is.

I'm still sorting out how I want to handle this from an architecture perspective. The general idea is kinda like what the parser does already;
it follows a sort of "grammar" that sets up a space of possibilities and expectations for what the type of a node should be based on the nodes around it.


**- Without any sort of Intermediate Representation (IR), any changes to your syntax trickles down into codegen.**

I'm gonna admit that I didn't really realize this one until encountering it directly. Until taking on this project, I wasn't really sure what the point of IR was besides doing your own optimizations, and my choice was to let LLVM or Cranelift worry about that.

But the real benefit of IR is that it's a stable interface between the frontend and the backend. If have an expressive enough IR, you'd be able to change or add features to your language without needing to make a special case for it in the codegen phase.

An example that really helped me understand this was the difference between loops like `for`, `while`, and `do-while`. In my current setup, each of these would be represented by a different Statement variant, and would need to be handled seperately during codegen. But these loops aren't super different in how they behave; their behavior can mostly be defined by much simpler language features to reduce duplication.

For example, the construction of a `while` loop would look something like this:

```
label loop_start:
    evaluate the condition
    if condition is false, jump to loop_end

    evaluate the body
    jump to loop_start

label loop_end:
    ...
```

And a `do-while` loop would look like this:

```
label loop_start:
    evaluate the body
    evaluate the condition
    if condition is true, jump to loop_start

label loop_end:
    ...
```

When you are doing code generation directly from the AST, you'd need to handle these two cases seperately, but looking at the way the loops are constructed, you can see that they're mostly the same, and only differ in where the condition is evaluated.

So in order to be able to handle a `for`, `while`, and `do-while` loop in the frontend, your middle-end IR just needs to be able to represend and infinite loop, and an if statement. For example:

```rust
// while loop
loop {
    if $condition break;
    $body
}

// do-while loop
loop {
    $body
    if $condition break;
}

// for loop
loop {
    $init
    if $condition break;
    $body
    $update
}
```

Using an IR that can express loops like this, my language might only have one of these loop types, but implementing the others would be as simple as generating a different ordering of a much simpler set of instructions.

Now that I see the point of IR, I know that its a necessary step in the pipeline, but its not gonna be an easy retrofit. Now that I have a mostly functioning language, inserting a lowering step in the middle is gonna be very difficult, and I'm still thinking about how to properly go about it.

At this point in the project, I have basically completely stopped working on it so I can do a lot of research and learning about the academics of compiler design.
I'm betting that it will be on-pause for a long while, but I'm excited to get over the hurdle and start making some of the features I've been most excited to explore.

When I get closer to that point, I hope to write some posts about some of the things that might set this language apart from others.
