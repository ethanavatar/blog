+++
title = "Thoughts on Type Inference"
draft = true
+++

Recently, I read the article [Type Inference Was a Mistake](https://borretti.me/article/type-inference-was-a-mistake).
While I might parrot the title on occasion, I disagree with some of the author's arguments.

<!-- more -->

### Re: Type Inference Makes Code Less Readable

The author argues that type inference creates too much of a reliance on language servers to reason about code,
and that it becomes more difficult to understand in places like a Git diff, blog post, or a vanilla text editor.

While I agree that a language should not be designed with the assumption that there is always a language server available,
I don't think that type inference has much to do with needing to look up what type a variable is.

Consider the following:

```rust
let d = get_direction();
// vs.
let d: Vector2 = get_direction();
```

What's the real difference here? I would argue that there isn't one. Thanks to the aptly named `get_direction`, in both cases, I know that `d` is a direction.

Now, suppose the declaration is not easily accessible and I see the following:

```rust
d = -d;
```

Now, I might be wondering what the type of `d` is.
I could use my language server to find out that `d` is a `Vector2`, so now I can infer myself that it's a direction and it is being flipped.

The problem with this example is that I might not have enough context to know what `d` is in the places where its being used,
and that doesn't change whether or not the declaration has a type annotation.
The declaration only happens once, but the variable may be used everywhere, and thats where I actually need to know what the variable is.

If knowing the type of a variable were so important for being able to understand what it is, maybe language design would have landed on something like this:

```rust
d: Vector2 = -d: Vector2;
```

But actually, I don't need to know type at all, I just need to know what it represents in order to know why its being negated.
So why not just give it better name to begin with?

```rust
direction = -direction;
```

Now I don't care what the type of the variable is, as long as I know its intent as well as the intent of the operation being performed on it.
The declared type is merely an implementation detail when it comes to understanding what the code does at a conceptual level.

### Re: In OCaml, Type Inference is a Footgun

I haven't written a lot of OCaml, so take this with a grain of salt.

The crux of the argument is that constraint solving can accept solutions that are in the programmer's blind spot for what they expected.
This is a problem that can exist in all inference systems, but it's made much worse in whole-program inference systems like OCaml's,
and the author argues that it is generally way easier to reason about code when inference is local to a function's implementation.

Although I cant think of a scenario in which I would encounter an issue like this in OCaml, I think this is a good point.
I also think this argument can be extended to other languages that have both generic types and function overloading.

C++, which is well known for its footguns, has both of these features.
Using templated parameters and overloaded functions is a recipie for disaster.
Especially in combination with `auto` variables,
a mis-selected overload can lead to an unexpected value making its way any distance through the program
and away from the actual source of the problem.

For example:

```cpp
// `-std=c++20` or `-fconcepts` for inferred parameters
int f(auto t) {
    return 1;
};

int f(std::string s) {
    return 2;
};

int main(void) {
    return f("");
}
```

This program will return `1`, because the compiler will infer `T` to be `const char*` and select the first overload,
and it is really easy to assume that the second would be picked because string literals
are often used in contexts where they are converted implicitly to `std::string`.

Footguns like this are always bad, and unfortunately the only real solution (aside from switching languages)
is to always consider their existence, and to try not to write yourself into that corner.

### Re: Type Inference Wastes Academic Effort

I could go both ways on this one.

### Re: The Whole Idea is Backwards

This one comes off pretty hot, but I don't think it's a bad point at all.

> I don’t want to infer types from my code. I’d rather infer the code from the types. Types are the spec...

Well said.


