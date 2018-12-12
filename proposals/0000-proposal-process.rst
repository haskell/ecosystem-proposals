A Proposal for Proposals
========================

.. contents::

Recently `GHC Proposals<https://github.com/ghc-proposals/ghc-proposals>`_ was
instituted, and seems to be a success, in giving all interested parties a voice
in proposed changes to GHC.

As there is a wider ecosystem around Haskell, in particular package curation,
discovery and management, this proposal process is proposed to similarly provide
a constructive venue for discussion around it.

Note that this document is *proposing* a process, it is not describing some sort
of official process for getting change to occur in the Haskell ecosystem. We are
humbly proposing it to you, dear member of the Haskell community, as a way to
rally forces around your ideas so that it gets done. Feel free to use a
different process if you think it has a better chance of success.

Motivation
----------

As Haskell has matured and started getting wider acceptance and use, the layer
of ecosystem beyond the raw compiler has started to receive attention.

In particular, there are now at least two end user package management tools,
`cabal-install` and `stack`. These in turn make use of backends which are
developed separately, and there is no overall community view or guidance as to
the direction these follow.

Proposed change
---------------

We propose a variant on the
`GHC Proposals <https://github.com/ghc-proposals/ghc-proposals>`_,
namely to use a GitHub repository containing accepted proposals, and to use its
pull request mechanism as a forum to discuss proposed changes. Unlike the GHC
Proposals process, there is no committee acting as a final arbiter of proposal
acceptance, because we recognize that changing the ecosystem requires buy-in
from all the involved parties, it cannot be imposed by a committee.

Proposal process
~~~~~~~~~~~~~~~~

Each proposal goes through the following stages:

1. The process begins with the opening of a pull request to the ecosystem proposals
   repository, proposing the merge of a document (derived from a
   `provided template <https://github.com/haskell/ecosystem-proposals/blob/master/proposals/0000-template.rst>`_)
   specifying the proposed change. This document is the primary specification
   of the feature.

   Due to GitHub's in-place editing feature (the pencil icon visible when viewing
   a file on GitHub), proposals can be made quickly without manual forking
   or cloning.
   
2. Community members (including representatives of the projects who will
   implement the proposed change) will discuss
   the proposal. The submitter is responsible for amending the specification to
   account for collected comments. It should be expected that the proposal will
   change during this process, which may last from days to months.

3. When the author feels that all the relevant representatives are on board with
   the proposal, and that the proposal would not be improved by further
   discussion, they can write a comment indicating that they consider the
   proposal accepted.

4. One of the maintainers of this GitHub repository will then mark the proposal
   as accepted by merging the pull request, and the
   document will be preserved in the proposals repository as a permanent
   specification for the feature.
   
5. The author will create github issues on the appropriate ecosystem components,
   linking to the proposal to provide a place track the progress of the
   implementation.

6. The author may choose to implement the proposal after acceptance, but she is
   under no obligation to do so. (Of course, neither is anyone else. This is why
   it is important to get buy-in first.)

7. During implementation, it is very likely that the specification will be refined.
   The implementor should keep the specification up to date over the course of
   the implementation.


Criteria for new features
~~~~~~~~~~~~~~~~~~~~~~~~~

When proposing or discussing a change, please take all of the following into
account.

1. *The problem*. What exactly is the problem that the feature solves? Is
   it an important problem, felt by many users, or is it very specialised?

2. *The right solution; generality*. Elegance, economy, and generality are
   important. Sometimes a problem has lots of solutions, none of which have that
   "aha" feeling of "this is the Right way to solve this". A classic example is
   that of records, for which we have had endless proposals (including many from
   the GHC authors themselves) none of which felt "right", and none of which
   made it into GHC.

3. *Fit with the ecosystem*. If we just throw things into the ecosystem
   willy-nilly, it will become a large ball of incoherent and inconsistent mud.
   Strive to add features that are consistent with the rest of the ecosystem.

4. *Specification cost*. Does the benefit of the feature justify the extra
   complexity? Does the new feature interact awkwardly with existing features,
   or does it enhance them? How easy is it for users to understand the new
   feature?

5. *Implementation cost*. How complex is the implementation likely to be? Is it
   highly localised, or does it require pervasive changes? As an author and
   contributor, it may look like you are giving the community free work, but this
   viewpoint doesn't align with the reality of a large project with a timescale
   in decades. Writing code is cheap; maintaining it is expensive.


Drawbacks
---------

Of course, group decision-making processes are difficult to manage and tools
will only bring you so far. While the Rust scheme does seem to function more
smoothly than our current system, it is not free of issues (as most recently
discussed by `Aaron Turon
<https://aturon.github.io/blog/2016/07/05/rfc-refinement/>`_). These issues will
likely apply to the process proposed here as well. In particular,

* GitHub discussions in particular don't scale terribly well; the lack of
  hierarchical threading means that long threads can become difficult to follow;
  experience suggests that Phabricator seems to be a bit better but long
  technical discussions are a challenge for nearly any tool.

* The ease of commenting may bring a slightly diminished signal-to-noise ratio
  in collected feedback, particularly on easily bike-shedded topics.


Alternatives
------------

There are a few alternatives which are worth considering,

* Adopting the process discussed above but replacing GitHub with GitLab. GitLab
  has many of the features of GitHub but with the advantage of being open-source
  and self-hostable. Unfortunately it would mean introducing yet another tool
  into the GHC developer's toolbelt and add yet another piece of infrastructure
  to administer.

* We move to something closer to the Python PEP scheme. Here a committee is
  formed for each proposal; the committee is responsible for crafting and
  collecting feedback on the proposal. The final acceptance decision is made by
  the Benevolant Dictator for Life. Discussion can be carried out on a medium
  of the committee's choosing, with a common choice being a specially-created
  mailing list.

* The Rust community has been `considering
  <https://aturon.github.io/blog/2016/07/05/rfc-refinement/>`_ breaking their
  process up in multiple stages to make their proposal queue more manageable. To
  first order these stages are,

  1. form a consensus around the problem and the need to solve it
  2. propose and refine possible solutions
  3. choose from among the proposed solutions

  The separation of step (1) from the others gives the community a means of
  concentrating focus on a set of small problems and encouraging exploration
  down multiple solution avenues. The cost of this is that it may frustrate
  authors with a slower, more involved process.

* Something else entirely...


Moving closer to the Rust process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Also, there are a few facets of the Rust process which the proposed process does
not carry over for a variety of reasons:

* *Shepherds*. In the Rust process each submitted proposal is assigned a
  shepherd. This is a trusted core developer who is charged with keeping the
  proposal moving through the process. At the moment GHC arguably lacks the
  contributor pool to guarantee this.

* *Final comment period*. The Rust process defines a portion of the proposal
  lifecycle known as the "final comment period". This is a (typically one-week)
  period directly before the responsible sub-team makes its decision which is
  widely announced to solicit final comments from the community. This period is
  omitted from the process described above; instead it is up to the proposal
  submitter to ensure that sufficient discussion is solicited.

Open Questions
--------------

There are still questions regarding the desired scope of the process. While we
want to ensure that changes which affect the user-facing aspects of the compiler
are well-considered, we certainly don't want the process to become unduly
burdensome. This is a careful balance which will require care to maintain moving
forward.

Acknowledgments
---------------

Thanks to the GHC Proposals contributors, as well as Herbert Valerio Riedel
 and Michael Snoyman for discussions about the concept of the process.
