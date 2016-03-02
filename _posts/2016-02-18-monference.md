---
title: A neural network is a monference, not a model
tags: [draft]
---

The distinction between _models_ and _inference procedures_ is central to most
introductory presentations of artificial intelligence.  For example: HMMs are a
class of model; the Viterbi algorithm is one associated inference procedure,
the forward--backward algorithm is another, and particle filtering is a third.

Many people describe (and presumably think of) neural networks as a class of
models. I want to argue that this view is misleading, and that it is more useful
to think of neural networks as hopelessly entangled model--inference pairs.
"Model--inference pair" is a mouthful, and there doesn't seem to be good
existing shorthand, so I will henceforth refer to such objects as "monferences".
My claim is that we should think of a neural network is an example of a
monference. (An implementation of the Viterbi algorithm, equipped with the
parameters of some _fixed_ HMM, is also a monference.)

I'm about to cite a bunch of existing papers that follow naturally from the
neural-nets-as-monferences perspective---it seems like this idea is already
obvious to a lot of people. But I don't think it's been given a name or a
systematic treatment, and I hope others will find what follows as useful
(or at least as deconfounding) as I did.

---

What are the consequences of regarding a neural net as a _model_?
A personal example is illustrative:

The first time I saw a recurrent neural network, I thought "this is an
interesting model with a broken inference procedure". A recurrent net looks like
an HMM. An HMM has a discrete hidden state, and a recurrent net has a
vector-valued hidden state.  When we do inference in an HMM, we maintain a
distribution over hidden states consistent with the output, but when we do
inference in a recurrent net, we maintain only a single vector---a single
hypothesis, and a greedy inference procedure. Surely things would be better if
there were some way of modeling uncertainty? Why not treat RNN inference like
Kalman filtering?

This complaint is _wrong_. Our goal in the remainder of this post is to explore
why it's wrong.

---

Put simply, there is no reason to regard the hidden state of a
recurrent network as a single hypothesis. After all, a sufficiently large hidden
vector can easily represent the whole table of probabilities we use in the
forward algorithm---or even represent the state of a particle filter. We will
show this experimentally in a moment. The analogy "HMM hidden state = RNN hidden
state" is bad; a better analogy is "HMM _decoder_ state = RNN hidden state".

This _temptation to form false analogies_ is especially appealing to those of us
who grew up in the graphical models culture, and are accustomed to inference
design problems that look algorithmic. But it's only one of a variety of failure
modes associated with the neural-nets-as-models perspective. Another
failure mode seems to preferentially afflict people from the neural nets
culture, who have never needed to think about inference at all: this is a
_failure to reason about computation_. 

I don't want to pick on anyone individually. But there seems to be a recent
trend of papers that start with a basic RNN, observe that it can't solve some
simple algorithmic or reasoning problem, and conclude that some crazy new
architecture is necessary---when often it would have been enough to let the RNN
run for more steps, or make a minor change to kind of recurrent unit used.  I
think people get in the habit of saying "everything is a function approximator,
and all function approximators are basically comparable". Whereas if you say
"everything is a program", these fair comparison issues become more complicated:
you have to start worrying about equal runtimes, availability of the right
floating point operations, etc. But when building inference procedures, these
are exactly the questions we should worry most about!

---

Let's look a little bit more closely at the case of hidden Markov models. Code
for experiments in this section can be found in the accompanying [Jupyter
notebook](https://github.com/jacobandreas/blog/blob/gh-pages/notebooks/monference.ipynb).

If we think about the classical inference procedure with the same structure as a
(uni-directional) recurrent neural network, it's something like this: for $$t =
0..n$$, receive an emission $$x_t$$ from the HMM, and _immediately_ predict a
hidden state $$y_t$$. You should be able to convince yourself that if we're
evaluated on tagging accuracy, the min-risk monference (if HMM parameters are
known) is to run the forward algorithm, and predict the tag with maximum
marginal probability at each time $$t$$. 

I generated a random HMM, drew a bunch of sequences from it, and
applied this min-risk classical procedure. I obtained the following
"online tagging" accuracy:

{% highlight text %}
    62.8
{% endhighlight %}

Another totally acceptable (though somewhat more labor-intensive) way of
producing a monference for this online tagging problem is to take the HMM, draw
many more samples from it, and use the (observed, hidden) sequences as training
data (x, y) for a vanilla RNN of the following form:

<img src="figures/monference_rnn.png" style="width: 30%">

(where each arrow is an inner product followed by a ReLU or softmax). In this
case I obtained the following accuracy:

{% highlight text %}
    62.8
{% endhighlight %}

Of course, we know that we can get slightly better results for this problem by
running the full forward-backward algorithm, and again making max-marginal
predictions. This improved classical procedure gave an accuracy of:

{% highlight text %}
    63.3
{% endhighlight %}

better than either of the online models, as expected. Training a bidirectional
recurrent net

<img src="figures/monference_bdrnn.png" style="width: 30%">

on samples from the HMM gave a tagging accuracy of:

{% highlight text %}
    63.3
{% endhighlight %}

See the pattern?  Notice: the neural nets we've used here don't encode anything
about classical message-passing rules, and they definitely don't encode anything
about the generative process underlying an HMM. Yet in both cases, the neural
net managed to achieve accuracy as good as (but no better than) the classical
message passing procedure with the same structure.

---

Neural networks are not magic! When our data is actually generated from an HMM,
we can't hope to beat an (information-theoretically optimal) classical
monference with a neural one. But we can empirically do just as well. Better
yet, by modeling our networks after the _algorithmic structure_ of classical
inference procedures, we can perhaps worry less about harder cases, when we
previously would have needed to hand-tune some approximate inference scheme.  As
we augment neural architectures to match more powerful inference procedures,
their performance improves.  Bidirectional recurrent nets are better than
forward-only ones; bidirectional networks with [multiple layers between each
"real" hidden vector](http://arxiv.org/abs/1602.08210) might be even better for
some tasks.

So far we've been looking at sequences, but analogues for more structured data
exist as well. For tree-shaped problems, we can run something that looks like
the [inside algorithm over a fixed
tree](http://www.socher.org/uploads/Main/SocherBauerManningNg_ACL2013.pdf) or
the [inside--outside algorithm over a whole sparsified parse
chart](https://aclweb.org/anthology/D/D15/D15-1137.pdf).  For arbitrary graphs,
we can apply repeated ["graph
convolutions"](http://arxiv.org/pdf/1509.09292.pdf) that start to look a lot
like belief propagation.

There's a general principle here: anywhere you have an inference algorithm that
maintains a distribution over discrete states, instead: 

1. replace {chart cells, discrete distributions} with vectors
2. unroll the "inference" procedure for a suitable number of iterations
3. train via backpropagation

The resulting monference has at least as much capacity as the corresponding
classical procedure. To the extent that appproximation is necessary, we can (at
least empirically) _learn_ the right approximation end-to-end from the training
data. 

(The version of this that backpropagates through an approximate inference
procedure, but doesn't attempt to learn the inference function itself, has [been
around](http://cs.jhu.edu/~jason/papers/#stoyanov-ropson-eisner-2011)
for [a while](http://www.cs.cmu.edu/~mgormley/papers/gormley+dredze+eisner.tacl.2015.pdf).)

I think there's at least one more constituency parsing paper to be written
using all the pieces of this framework, and lots more for working with
graph-structured data.

---

I've argued that the monference perspective is useful, but is it true? That is,
is there a precise sense in which a neural net is _really_ a monference, and not
a model?

No. There's a fundamental identifiability problem---we can't really distinguish
between "fancy model with trivial inference" and "mystery model with complicated
inference". Thus it also makes no sense to ask, given a trained neural network,
which model it performs inference for. (On the other hand, networks trained via
[distillation](http://arxiv.org/abs/1503.02531) seem like good candidates for
"same model, different monference".) And the networks-as-_models_ perspective
shouldn't be completely ignored: it's resulted in a fruitful line of work that
replaces log-linear potentials with little neural networks [inside
CRFs](http://www.eecs.berkeley.edu/~gdurrett/papers/durrett-klein-acl2015.pdf).
(Though one of the usual selling points of these methods is that "you get to
keep your dynamic program", which we've argued here is true of regular recurrent
networks as well.)

In spite of all this, as research focus in this corner of the machine learning
community shifts towards [planning, reasoning, and harder algorithmic
problems](http://nips2015.sched.org/event/4G4h/reasoning-attention-memory-ram-workshop),
I think the neural-nets-as-monferences perspective should dominate. 

More than that---when we look back on the "deep learning revolution" ten years
from now, I think the real lesson will be the importance of end-to-end training
of decoders and reasoning procedures, even in systems that [barely
look
like neural networks at all](http://arxiv.org/abs/1601.01705). So when building
learning systems, don't ask: "what is the probabilistic relationship among my
variables?". Instead ask: "how do I approximate the inference function for my
problem?", and attempt to learn this approximation directly. To do this
effectively, we shouldn't ignore everything we know about classical inference
procedures. But we should also start thinking of inference as a first-class part
of the learning problem.

---

Thanks to Robert Nishihara and Greg Durrett for feedback.
