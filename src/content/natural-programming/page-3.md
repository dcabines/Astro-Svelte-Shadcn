## Quick Overview

This is a quick overview of the topics in this book.

### Functional Programming

Imperativity in programming is legitimate, for optimization of execution frugality. But in higher
level programming, with tracing garbage collection: execution of functional sourced programs
are usually not less frugal than of imperative programs. Hence at higher level: side effects are
just unnecessary complication, ubiquitously using them is so stupid as ubiquitously using the
'goto' instruction in a language like C, instead of the structured execution flow control. Still, in the industry, even with tracing garbage collection: many programming languages [Java,
C#, ...] were designed to be dominantly imperative. This was just idiotic decision.
Unfortunately software coders naively believed that this was legitimate programming
language design and that they ought to accept it and tilt their thinking to it. Thus the coding
culture followed the programming language style, it also became imperative, side-effects are
now ubiquitous, even without any practical reason, just as a habit. This greatly contributed to
why the average quality of the software code now is tragicomically low.

This book serves also as an introduction to functional programming.

### The Type System

#### Strength

The static type-system of most industrial languages is too weak. The biggest poblem is the
absense of type-function polymorphism ["higher kinded types"]. This book shows why this
feature is valueable, via the most important use-cases.
Paradigm

Unlike the wide-spread industrial languages: the type systems of Haskell-like languages are
based on mathematical type theory. Harnessing the research work, done by mathematicians
for decades: we get natural, simple, reliable and expressive type systems for programming
languages.

#### Type Interface System

The invokations of the methods of type interfaces can be dispatched either in compile-time or
in run-time. The "object oriented" option is the run-time one, which is idiotic design decision
for a statically typed language, this book will show why. Haskell dispatches in compile-time.