# Computational aesthetics for foundations of math
## 2008-09-29

A foundation for mathematics is a formal system (language + logic) in which all other formal systems can be expressed and reasoned about.
By Goedel's first incompleteness theorem, such systems are never logically complete (with finite axiomatizations).
Thus any foundation of math leaves some questions unanswered.
Logicians must ask the ongoing question “what new axioms should be assumed”.
So let us ask,

What new axioms should be assumed [in any foundation of math]? Of course no algorithm can decide which axioms to add, otherwise we could simply add a finite axiomatization of the algorithm.
What new axioms should be assumed [in any foundation of math]? Of course no algorithm can decide which axioms to add, otherwise we could simply add a finite axiomatization of the algorithm.
Instead logicians, e.g. professional set theorists, employ the aesthetic rule: “good axioms lead to elegant theories”.
So what is an elegant theory? In elegant theories, the world is simple: sensible things are easy to say, and senseless jabber is difficult to say.
The mathematical literature itself serves as a data set of sensible statements, expressed as sets (as e.g. in a Kieffer et al. <a href="#1">[1]</a>).
So elegant theories should simply shrink the remaining [by contrast, senseless] part of the universe of sets to be as small as possible.

Which axioms shrink the remaining universe? What is a small model of the universe of sets? In our present application, we can formalize by defining a notion random set, and minimizing the universe's entropy (a soft notion of size).
Since we're interested in writing simple math, let's generate random sets by picking random expressions denoting sets.
Formally, we define a probabilistic grammar, whose parameters are statistically fit to a corpus of real-world expressions (the mathematical literature).
Then we can simply rank axiom candidates by the entropy change they induce on the universe of sets.

This aesthetic algorithm works in theory, but founding math in set theory leads to practical difficulties: sets have a complicated syntax (it's even undecidable whether a given set expression is actually a set), and complicated reasoning principles.
The grammatically-simplest foundation for computable mathematics is arguably [Combinatory Logic](http://en.wikipedia.org/wiki/Combinatory_logic), a language with two constants and a single binary operation.
In fact combinatory algebra can be extended by a couple more constants, and a few more axioms, so that all mathematical questions can be posed as equations between these extended terms.

My [Ph.D. research](http://fritzo.org/thesis.pdf) focussed on implementing and assessing the min-entropy aesthetic algorithm, and working on the particular foundation of an extended combinatory algebra.

- [1] <a name="1"/>
  Steven Kieffer, Jeremy Avigad, Harvey Friedman (2009)
  "A language for mathematical knowledge management"
  [(pdf)](http://logika.uwb.edu.pl/studies/download.php?volid=31&artid=sk&format=PDF)
