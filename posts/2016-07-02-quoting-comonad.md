# A computational comonad for quoting
## 2016-07-02

Suppose you're writing a library in a language with macros (e.g. in Lisp),
and you want to be able to refactor your library without breaking user code.
Could the language designers guarantee safety by baking constraints into the language's quoting interface?

Consider the spectrum of quoting interfaces, from unsafe to safe.
On the unsafe end of the spectrum, users have full access to source, and no changes are safe.
Lisp is on the unsafe end.
On the safe end of the spectrum, users can only evaluate your code, and you can safely replace any chunk of code with a Scott-equivalent chunk of code.
In the middle of the spectrum, we could consider quoting modulo a weak notion of equality.
For example, quoting modulo alpha-equivalence would safely permit you to rename-refactor your library.

Let's define a quoting interface in the form of a _computational comonad_ <a href="#1">[1]</a> (in [Coq](https://coq.inria.fr/) syntax):

```coq
Quoted : type -> type.
lift : forall (t1 t2:type), Quoted(t1->t2) -> Quoted t1 -> Quoted t2.
eval : forall (t:type), Quoted t -> t.
{-} : forall (t:type), t -> Quoted t.
quote : forall (t:type), Quoted t -> Quoted(Quoted t).
```

where `Quoted` and `{-}` are in the meta language,
and `lift`, `eval`, and `quote`, are in the object language
(`quote` is just the object-level version of `{-}`).
We require equations

```coq
forall (t:type) (x:t), eval{x} = x.
forall (t:type) (x:Quoted t), eval(quote x) = x.
forall (t:type) (x:Quoted t), quote{x} = {{x}}.
forall (t1 t2:type) (f:t1->t2) (x:t1), lift{f}{x} = {f x}.
```

Note that in terms of a Kleisli triple, the pair `(Quoted,lift)` is the functor,
`eval` is the counit, and we can define the cobind operator by

```coq
cobind : forall (t1:type) (t2:type),
  (Quoted t1 -> t2) -> Quoted t1 -> Quoted t2.
cobind t1 t2 f x := {f x}.
```

This `cobind` is in the meta language, not the object language, but we can define a more convenient object version

```coq
cobind' : forall (t1:type) (t2:type),
  Quoted(Quoted t1 -> t2) -> Quoted t1 -> Quoted t2.
cobind' f x := lift(quote f)(quote x).
```

So far we can't do anything with the quoted code, except evaluate it.
It's enough to add an equality predicate (a Church delta) for quoted terms, assuming some notion of equality.

```coq
equiv : forall (t:type), Quoted t -> Quoted t -> bool.
```

The `equiv` operator is at the object level,
and returns the object level `bool`.
`equiv` makes each `Quoted` type into a numeral system
(a flat domain with a Church delta),
and we can define all sorts of safe macros that transform quoted code.

We can tune the safety of our `Quoted` comonad by tuning the coarseness of this `equiv` operator.
In <a href="#2">[2]</a>, I explored the extreme safe end of the spectrum: quoting modulo Scott-equality.

## References

- [1] <a name="1"/>
  Stephen Brookes, Shai Geva (1991)
  "Computational Comonads and Intensional Semantics"
  [(pdf)](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.45.4952&rep=rep1&type=pdf)
- [2] <a name="2"/>
  Fritz Obermeyer (2009)
  "Automated Equational Reasoning in Nondeterministic &lambda;-Calculi Modulo Theories H∗"
  [(pdf)](http://fritzo.org/thesis.pdf)
