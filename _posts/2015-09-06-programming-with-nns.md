---
title: Programs made of neural networks
---

A crude history of applied machine learning:

> Whenever we have a low-capacity model with hand-engineered structural
> constraints, and replace it with a high-capacity model with simple features
> and few structural constraints, model quality improves [models are smaller,
> take less time to develop, and generalize better to unseen data].

See (in NLP): linear models replacing decision lists, Jelinek's infamous
linguists, statistical machine translation, the recent flurry of papers whose
entire substance is "replace this log-linear model (a two-layer neural net) with
a three-layer neural net".

A crude history of programming languages:

> Whenever we have a programming language with lots of simple constructs, and we
> replace them with a few high-level constructs, program quality
> improves [programs of equivalent complexity are shorter, take less time to
> develop, and are less likely to contain bugs].

First everyone stopped writing assembly, then everyone stopped writing C.[^1]

Notice: in each case we're moving the same slider---just moving it in different
directions. Machine learning and programming language design ultimately have the
same goal: making it as easy as possible for certain problem-solving machines
(whether those are humans or optimization algorithms) to produce correct code
according to some specification.  Out in the real world, we don't favor machine
learning because it is inherently more pure or beautiful than writing code by
hand---we use it because it's _effective_. If somebody released a library today
with a bunch of composable vision primitives, and suddenly Facebook to could
solve all their image-labeling problems more effectively with interns rather
than neural nets, then neural nets would be out the door tomorrow.

Actually, can we write this library now?

To be clear, I don't mean something like OpenCV, where you take a bunch of
pre-implemented models for particular tasks and then do whatever
stitching-together you want in postprocessing. Instead, again, some notion of
little vision primitives from which it would be possible to write a classifier
as

{% highlight scala %}
    load(image) andThen 
      detectObjects andThen 
      orderBy(salience) andThen 
      head andThen 
      name
{% endhighlight %}

or a captioner as

{% highlight scala %}
    load(image) andThen 
      detectObjects andThen 
      describeAll
{% endhighlight %}

or a face detector as

{% highlight scala %}
    load(image) andThen 
      detectObjects andThen 
      filter(name(_) == Face) andThen 
      drawBoundaries
{% endhighlight %}

What do the functions `detectObjects`, `describeAll`, etc. look like? Current
experience suggests that they should be neural nets, but neural nets of a very
particular kind: rather than being trained to accomplish some particular task
(like image captioning), they're trained to be freely composable: `describeAll`
promises to take anything "like a list of detections" (whether directly from
`detectObjects` or subsequently filtered) and produce a string. Note in
particular that the inputs and outputs to these functions are all real
vectors. There is no way to structurally enforce that a thing "like a list of
detections" actually has the desired semantics, and instead we rely entirely on
the training procedure.

In current real-world implementations, there's a notion of _layers_ as modular,
pre-specified units, but _networks_ as monolithic models customized for specific
tasks (and requiring end-to-end training). Once we move to modular networks,
though, we can start to perform tasks for which _no training data exists_. For
example, "write a caption about the people in this image":

{% highlight scala %}
    load(image) andThen 
      detectObjects andThen 
      filter(name(_) == Face) 
      andThen describeAll
{% endhighlight %}

using only the primitives specified above! 

Steps we are already taking in this direction: the fact that people use a prefix
of an image classification network to initialize models for basically every
other vision task; the fact that "attention" is suddenly being treated as a
primitive in model descriptions even though it's a complicated sequence of
operations for combining multiple layers. Roger Grosse's beautiful [paper on
grammars over matrix factorization
models](http://www.cs.toronto.edu/~rgrosse/uai2012-matrix.pdf) also kind of
looks like this, and Christopher Olah has a [discussion of the type-theoretic
niceties](http://colah.github.io/posts/2015-09-NN-Types-FP/) of neural nets
understood as collections of reusable modules (though to me this seems largely
secondary to the practical question of what these types are).

To bring this back to the earlier programming language discussion, we observe
that:

1. It's hard for a person to write down a person-detector by hand, but easy for
   a neural net.

2. Given appropriate functional vision primitives, it's easy for a person to
   write down a person _describer_. But training a neural net to do this from
   scratch requires a lot of examples of people descriptions to do this.  (We
   might then say it's "easy" for people but "hard" for a neural net.)

To take this yet a step further, we can note that there are lots of machine
learning techniques that are more human-like than neural-net-like, in the sense
that they do well with tiny data sets and a good pre-specified inventory of
primitives (e.g. program induction, semantic parsing). If we really just care
about minimal human intervention, we can figure out our vision primitives and
then hand them off to a machine learning subsystem of an entirely different
kind.

So let's write this library!  There are research questions here: First, what is
the right set of functional primitives to give people (or models for program
induction)? Next, can these shared representations actually be learned? How do
we find parameter settings for these modules using the kinds of labeled data
currently available?

Disclosure: I already have a model like this working on a bunch of simple
question-answering tasks about images---I think it's a really exciting
proof-of-concept, and I'll hopefully be able to show it off soon. But it's not a
comprehensive solution (esp. if we want to interface between vision / language /
control applications), and I think there's a really interesting systems problem
here too.

---

Followup:

* [Deep compositional question answering with neural networks](http://arxiv.org/abs/1511.02799)
* [Learning to compose neural networks for question answering](http://arxiv.org/abs/1601.01705)


[^1]: Obviously this is a gross overstatement, since lots of people do continue to
      write assembly and C. But I think it's less controversial to say that _fewer_
      people write in low-level languages, and that it's harder to do so correctly.
