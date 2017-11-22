---
title: "Lewis: General Semantics"
categories: [reading]
---

- Questions: "what sort of thing is meaning?", "how is it compositional?".

- Contrast with Katz "semantic markerese" [logical language?].

- Translating to Markerese doesn't require understanding truth conditions, but
  "semantics with no treatment of truth conditions is not semantics".

- Not about social use of language: "possible languages as abstract semantic
  systems" and "psychological and sociological facts whereby one of these
  systems is used by a population" are totally separate things. [But we have no
  example of the former divorced from the latter. All languages arise in social
  context, so presumably the actual form that meaning takes, the fact that it's
  approximately context free, the fact that meaning is compositional all arise
  from social factors.]

- This is in the model-theoretic tradition, but offers "a simpler way to do
  essentially the same thing".

- Underlying syntactic formalism is categorial grammar ["transformational" just
  means categories have ordering info?]

- "A meaning for a sentence is something that determines the conditions under
  which the sentence is true or false. It determines the truth-value of the
  sentence in various possible states of affairs, at various times, at various
  places, for various speakers, and so on."

- It follows that the intension of a sentence is a fn from indices to truth
  values, names: indices -> things, nouns, indices -> sets.

- Rather than fns of possible worlds (a la Carnap), take these indices to be
  coordinates: "packages of miscellaneous factors relevant to determining
  extensions"---includes not just id of possible world, but speaker location in
  place, time, bindings to indexicals, etc.

- "Intensions are designed to do part of what meanings do. Yet they are not
  meanings, for there are differences in meaning unaccompanied by differences in
  intension." (Tautologies, etc.) [Is it obvious that tautologies all have the
  same intension under a sufficiently rich system of coordinates? Not as given
  in the paper, but if the speaker's _beliefs_ are part of the coordinate
  system, different prior beliefs should distinguish different tautologies
  based on what the listener has computed so far. In general it's a little weird
  in these truth-conditional approaches that uncertainty is not part of the
  state for purposes of predictaion, since speakers and listeners obviously
  don't have access to deductive closure over even those parts of the world
  they observe. And once you have machinery for assigning binary truth values to
  indices, you're almost all the way to a full probabilistic treatment.]

- What is a "thing"? Russell's paradoxes exclude things like "all sets",
  "intensions". This paper doesn't treat with semantic metalanguages.

- An adj is a function from nouns to compound nouns. NOT: from sets of
  things to sets of things. Consider that _Maoist_ and _Communist_ might pick
  out the same set of things, but _alleged Maoist_ and _alleged Communist_
  different sets. [But then do we believe in compositionality at all? Intension
  of a constituent is determined by interactions among all the words in the
  constituent. The treatment here is superficially compositional, but if
  _alleged_ can freely do different things to different nouns then you haven't
  given up any expressive power.]

- More generally, the intension of a type (x/y..z) is a function from
  y..z-intensions to x-intensions. [What? If "Communist" and "Maoist" have the
  same extension in every index, they have the same intension (in "coordinate"
  sense). So does this defn of intension also carry lexical information?]

- We've said so far that "meaning" needs to be more than intension, at least to 
  distinguish between tautologies. So say "meaning" has something to do with
  structure as well: "Semantically interpreted phrase markers minus their
  terminal nodes". [So no pair of sentences with different syntax can have the
  same meaning?]

- Truth of an utterance is defined w/r/t a particular _occasion_, specified by a
  set of indices.

- Various notions stronger than truth are defined based on structural
  equivalence.

- Usual CCG observation that once we have made the category part of the meaning
  of the word, a grammar just specifies a way to encode meanings. Grammar just
  provides ordering information on top of types.

- Discussions of how ti implement various other syntactic theories in this
  framework. [???]

- L analyzes DPs as S/(S/N). What are you doing?

- Ah---to force quantifiers to scope in the right order. This seems like a weird
  conflation of a purely syntactic phenomenon with a semantic one.

- [Skipping details of discussion---an alternative analysis is offered that
  looks more normal]

- Non-declarative sentences: treat as paraphrases of the corresponding
  performative. [Yes!]

- Self-referential sentences generate situations where paraphrase is not
  truth-preserving.

---

One thing that really surprises me is the casualness with which L allows the
intension of _alleged Maoist_ to be determined by a combination of the _words_
_alleged_ and _Maoist_, and not by some regular combination of their intensions.
This distinction goes to the heart of why compositionality is hard to pin down,
and it's not resolved satisfactorily here. On one hand, it is indeed obviously
the case that [[_alleged Maoist_]] is not just [[_alleged_]] AND [[_Maoist_]].
On the other hand, if you allow modifiers to be arbitrary functions from the
phrases they modify to other intensions, you can assign any possible sequence of
meanings to any possible sequence of sentences---you've removed the possibility
of making any meaningful statement about compositionality in your language. If
we really believe that meaning is compositional, it has to be generated by
some mechanism stronger than intersection but weaker than the version presented
here; the interesting question is how much weaker.

On the subject of overpowered mechanisms: The notion that two utterances should
be regarded as having the same meaning only if they generate it via the same
tree-shaped computation seems initially like it's too restrictive. But once it
becomes clear that in this account "paraphrases" are generated by transformation
of some underlying deep structure rather than with new computations, it again
becomes arbitrarily powerful unless you're willing to put some restrictions on
the form of the transformational grammar. But in any case this seems like a lot
of machinery to introduce just to give different tautologies different meanings,
when you can resolve everything by putting the set of conclusions _available to
the listener_ into the coordinate system.

The account of non-declarative sentences seems correct.
