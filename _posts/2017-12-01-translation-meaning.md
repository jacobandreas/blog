---
title: "Quine: Translation & Meaning"
categories: [reading]
---

Problem we're trying to solve: could two people say the same words in all
situations but mean something different by those words?

Consider a speaker as a distribution p(sentence | context) for some set of
sentences and contexts. Claim: there exists a set of "accessible" contexts and
conditional distributions such that we can permute all the sentences and wind up
with the same p(sentence | context).


Alterantive way of asking the question: can we write a translation model that
generates appropriate utterances in all contexts but does not actually preserve
meaning?

[The weaker version of this---can we generate a bad translation phrasebook that
preserves p(s) in the source language?---is empirically false given the success
of translation-as-decipherment work.]

What's in a context? A whole history of observations. (But not straightforward
to disentangle this from experiences that define the language rather than its
use.)

A "linguist" observes only p(s | c), from which they wish to recover a mapping
from every s to some s' that is meaning-preserving. [In what sense of meaning?]
[Such a mapping is in any case not guaranteed to exist even for simple
extensional languages.]

So present a speaker with a stimulus, get them to respond yes or no; the set of
stimuli to which the speaker assents lets you identify the corresponding word.
(Q seems to imagine a more interactive process where the linguist begins with a
particular hypothesis about the translation.) [Compare to truth-conditional
accounts of semantics.]

"meaning, supposedly, is what a sentence shares with its translation" (32).
[This seems circular---how do we identify translations if we haven't first
identified what they should share? And if we also are happy with "translations"
being things we've elicited in the manner described above, then the elicitation
procedure defines meaning, not "translation".]

Q: exactly---call this the stimulus meaning. 

And versus Carnap: Framing this as a translation criterion avoids some of the
problems needed to prevent the word "unicorn" from being part of the truth
conditions for _unicorn_. [Arguably the spelling is part of the truth
conditions.] In this framework subjunctives cannot be achieved via stimulus; in
Carnap those judgments can be supplied by the speaker.

Distinguish between occasion sentences and standing sentences---the second don't
require stimulus of the kind above. [Does he just mean indexicals?]

Or, a standing sentence is just an occasion sentence but about past experience.

[Didn't we say that the relevant context for a stimulus includes a whole history
of observations? In this case, why isn't the initial stimulus followed by some
generic waiting period a "stimulus" for a standing sentence? Just that it's
outside the modulus.]

Obviously for purposes of elicitation it may be nontrivial for the linguist to
determine the speaker's full history.

Or, imagine a fly that always appears in the presence of rabbits [such that
natives don't have a word for "rabbit without fly"?].

Very important point: the stimulus meaning of "gavagai" includes moduli in
which a local has recently made the sound [gavagai]. The stimulus meaning of
"rabbit" includes moduli in which a local has recently made the sound
[ræbɪt] (but *not* [gavagaj]). So can never have perfect synonymy via
equivalence of stimulus meaning without some complicated operator that replaces
all language-like stimuli with their translated versions.

And, as noted above, we can't meaningfully distinguish between the case where a
sentence S picks out worlds $$W$$ but only worlds $$W' \subset W$$ upon
learning some additional piece of information $$C$$, and the case where S picks
out $$W'$$ to begin with.

Or, culture-dependent obeservation histories that would stun a speaker to
silence. [Not a problem with "what belief does this utterance induce?".]

For any two speakers whose social contacts are not virtually identical, the
stimulus meanings of "bachelor" will diverge far more than "rabbit". [But the
social contacts are part of the context used in computing stimulus meaning. So
maybe more straightforward to say in general that we'll always define meaning
w/r/t a particular initial belief assumed shared.]

Q's solution (basically equivalent): just do everything w/r/t stimulus meanings
for a single bilingual speaker. [Great, and also avoids problems with
rabbit-flies etc.]

Contextual info is still tricky---morning star vs evening star, etc.

---

Can stimulus meaning distinguish between a rabbit and a "temporal segment of a
rabbit" or "rabbithood"? Q: anything that stimulates the specific term also
stimulates the general one. [How can we ever learn anything about parts that
belong to wholes but are not recongizable outside of context? At least
definitionally; in the case of the bilingual speaker translating via stimuli, we
can use L1 as part of the stimulus to determine the meaning of an L2 word.]

[In any case if there's no stimulus that distinguishes "Rabbit segment." from
"Rabbit.", we might actually want to consider those sentences to be paraphrases
of each other, even if the composed sentences "He is eating a rabbit." and "He
is eating a rabbit segment." have different stimulus meanings. Cf "alleged
Maoist".]

For lots of words like "bachelor", only the definitional part is shared---no
two speakers will actually have the smae stimulus meaning. [This is why I like
the "what does this sentence make you believe" formulation rather than the "what
sentences are you willing to utter given this stimulus".]

---

It will be difficult to find analogues of logical operators, since:

- speakers may be imperfect reasoners and assent to statements that are logical
  contradictions

- natural languages don't actually have pure logical operators (consider Eng
  speaker answering a question "Yes and no.")

- incomplete information on part of speakers leads to problems with extensional
  judgments about truth conditions

That is, we can't identify translations of logical operators except via their
extension, but extensions are unreliable.

---

The trouble with synonymy: with a short modulus, any pair of speakers are likely
to be influenced by background knowledge in a way that makes it difficult to
determine equivalence on the basis of stimulus meaning. But with a sufficiently
long modulus [Q says a month but it seems like nothing short of a lifetime will
do in general] "there is no telling what to expect". [Is this just a statement
that there is uncertainty in the resulting distribution over responses? Can
compare distributions rather than binary judgment.]

Treatment of analyticity is substantially the same as synonymy (with sentenes of
the form _if p then p_).

---

Observation sentences, truth sentences, stimulus-analytic sentences can be
translated.

"Questions of intrasubjective stimulus synonymy of native occasion sentences
even of non-observational kind can be settled if raised, but the sentences
cannot be translated" (S15).

In general we expect a good translator to turn foreign sentences that are
analytic into native sentences that are analytic. But suppose we're working with
a people that regards the sentence "all rabbits are men reincarnate" as a
tautology? Problem is basically that we imagine our foreign and native speakers
to be working with different notions of deductive closure: if we assumed these
were the same some of our problems would be much easier.

Or even more strongly, by letting the language user be the same person for both
languages.

---

So what do we make of all this? Certainly true that as a practical matter we
can't generate all possible stimuli necessary to identify truth conditions for
every utterance in a language. 

More interesting possibility is for a single speaker of both languages: he has a
"private implicit system of analytical hypotheses"; another speaker could have
exactly the same speech dispositions in each language but a different
disposition to translation.

Question is: is the distinction between the translation model possessed by our
two speakers nontrivial? In the sense that e.g. someone relying on translations
will take different behaviors or form different beliefs about the state of the
world on the basis of these translations? Not clear that Q has provided a real
example of such a pair of languages, since the rabbit-vs-rabbit-stage
distinction can clearly be made on the basis of some (perhaps just imagined
stimulus), or else it isn't a distinction at all.

Of course, if we're only concerned with the speakers having the same disposition
w/r/t some subset of possible contexts (the "real ones"), then this
indeterminacy is certainly possible, but not an indeterminacy of translation so
much as an indeterminacy of language-learning _per se_ (as Q himself points out at
the end).

But if we actually have access to all possible contexts, we're back to the
initial problem: what does it look like to have p(s | c) s.t. we can permute s
and have everything be the same? 
