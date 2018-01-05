# Requests for Discussion

Based on the wonderful work made public by [Joyent](http://github.com/joyent/rfd).

Writing down ideas for system enhancement while they are still nascent
allows for important, actionable technical discussion.  We capture
these in **Requests for Discussion**, which are documents in the original
sprit of the [IETF Request for Comments](https://en.wikipedia.org/wiki/Request_for_Comments),
as expressed by [RFC 3](https://tools.ietf.org/html/rfc3):

> The content of a note may be any thought, suggestion, etc. related to
> the software or other aspect of the network.  Notes are encouraged to
> be timely rather than polished.  Philosophical positions without examples
> or other specifics, specific suggestions or implementation techniques
> without introductory or background explication, and explicit questions
> without any attempted answers are all acceptable.  The minimum length for
> a note is one sentence.

> These standards (or lack of them) are stated explicitly for two reasons.
> First, there is a tendency to view a written statement as ipso facto
> authoritative, and we hope to promote the exchange and discussion of
> considerably less than authoritative ideas.  Second, there is a natural
> hesitancy to publish something unpolished, and we hope to ease this
> inhibition.

The philosophy of our Requests for Discussion is exactly this: timely
rather than polished, with the immediate idea of promoting technical
discussion.  Over time, we expect that this discussion will often converge
on an authoritative explanation of new functionality -- but it's entirely
acceptable for an RFD to serve only as a vector of discussion.
(We use the term "Requests for Discussion" in lieu of "Requests for
Comments" to avoid conflation with the IETF construct -- and the more
formal writing that it has come to represent.)

## RFDs

| state    | RFD |
| -------- | ------------------------------------------------------------- |
| predraft  | [RFD 1 Spearhead Directory Service (LDAP)](./rfd/0001/README.md) |
| predraft  | [RFD 2 Spearhead DNS Service (DNS)](./rfd/0002/README.md) |

## Contents of an RFD

The following is a way to help you think about and structure an RFD
document. This includes some things that we think you might want to
include. If you're unsure if you need to write an RFD, here are some
occasions where it usually is appropriate:

* Adding new endpoints to an API or creating an entirely new API
* Adding new commands or adding new options
* Changing the behaviour of endpoints, commands, APIs
* Otherwise changing the implementation of a component in a significant way
* Something that changes how users and operators interact with the
  overall system.
* Changing the way that software is developed or deployed
* Changing the way that software is packaged or operated
* Otherwise changing the way that software is built

This is deliberately broad; the most important common strain across RFDs
is that they are technical documents describing implementation considerations
of some flavor or another.  Note that this does not include high-level
descriptions of desired functionality; such requests should instead phrased
as [Requests for Enhancement](./rfd/0102/README.md).

RFDs start as a simple markdown file that use a bit of additional metadata
to describe its current state. Every RFD needs a title that serves as a
simple synopsis of the document. (This title is not fixed; RFDs are numbered
to allow the title to change.) In general, we recommend any initial RFD
address and/or ask the following questions:

##### Title

This is a simple synopsis of the document. Note, the title is not fixed.
It may change as the RFD evolves.

##### What problem is this solving?

The goal here is to describe the problems that we are trying to address
that motivate the solution. The problem should not be described in terms
of the solution.

##### What are the principles and constraints on the design of the solution?

You should use this section to describe the first principles or other
important decisions that constrain the problem. For example, a
constraint on the design may be that we should be able to do an
operation without downtime.

##### How will users interact with these features?

Here, you should consider both operators, end users, and developers. You
should consider not only how they'll verify that it's working correctly,
but also how they'll verify if it's broken and what actions they should
take from there.

##### What repositories are being changed, if known?

If it's known, a list of what git repositories are being changed as a
result of this would be quite useful.

##### What public interfaces are changing?

What interfaces that users and operators are using and rely upon are
changing? Note that when changing public interfaces we have to be extra
careful to ensure that we don't break existing users and scripts.

##### What private interfaces are changing?

What interfaces that are private to the system are changing? Changing
these interfaces may impact the system, but should not impact operators
and users directly.

##### What is the upgrade impact?

For an existing install, what are the implications if anything is
upgraded through the normal update mechanisms, e.g. platform reboot,
sdcadm update, manta-adm update, etc. Are there any special steps that
need to be taken or do certain updates need to happen together for this

##### What is the security impact?

What (untrusted) user input (including both data and code) will be used as part
of the change?  Which components will interact with that input?  How will that
input be validated and managed securely?  What new operations are exposed and
which privileges will they require (both system privileges and Triton privileges)?
How would an attacker use the proposed facilities to escalate their privileges?


## Mechanics of an RFD

To create a new RFD, you should do the following steps.

### Allocate a new RFD number

RFDs are numbered starting at 1, and then increase from there. When you
start, you should allocate the next currently unused number. Note that
if someone puts back to the repository before you, then you should just
increase your number to the next available one. So, if the next RFD
would be number 42, then you should make the directory 0042 and place it
in the file 0042.md. Note, that while we use four digits in the
directories and numbering, when referring to an RFD, you do not need to
use the leading zeros.

```
$ mkdir -p rfd/0042
$ cp prototypes/prototype.md rfd/0042/README.md
$
```

### Write the RFD

At this point, you should write up the RFD. Any files that end in `*.md`
will automatically be rendered into HTML and any other assets in that
directory will automatically be copied into the output directory.

RFDs should have a default text width of 80 characters. Any other
materials related to that RFD should be in the same directory.

#### RFD Metadata and State

At the start of every RFD document, we'd like to include a brief amount of
metadata. The metadata format is based on the
[python-markdown2](https://github.com/trentm/python-markdown2/wiki/metadata)
metadata format. It'd look like:

```
---
authors: Han Solo <han.solo@shot.first.org>, Alexander Hamilton <ah@treasury.gov>
state: draft
---
```

We keep track of two pieces of metadata. The first is the `authors`, the
second is the state. There may be any number of `authors`, they should
be listed with their name and e-mail address.

Currently the only piece of metadata we keep track of is the state. The
state can be in any of the following. An RFD can be in one of the
following four states:

1. predraft
1. draft
1. publish
1. abandoned

While a document is in the `predraft` state, it indicates that the work is
not yet ready for discussion, but the RFD is effectively a placeholder.
Documents under active discussion should be in the `draft` state.  Once
(or if) discussion has converged and the document has come to reflect
reality rather than propose it, it should be updated to the `publish`
state.

Note that just because something is in the `publish` state does not
mean that it cannot be updated and corrected. See the "Touching up"
section for more information.

Finally, if an idea is found to be non-viable (that is, deliberately never
implemented) or if an RFD should be otherwise indicated that it should
be ignored, it can be moved into the `abandoned` state.

### Start the discussion

Once you have reached a point where you're happy with your thoughts and
notes, then to start the discussion, you should first make sure you've
pushed your changes to the repository and that the build is working.

From here, send an e-mail to the appropriate mailing list that best fits
your work. The options are:

* [sdc-discuss@lists.smartdatacenter.org](https://www.listbox.com/member/archive/247449/=now)
* [manta-discuss@lists.mantastorage.org](https://www.listbox.com/member/archive/247448/=now)
* [smartos-discuss@lists.smartos.org](https://www.listbox.com/member/archive/184463/=now)

The subject of the message should be the RFD number and synopsis. For
example, if you RFD number 169 with the title  Overlay Networks for Triton,
then the subject would be `RFD 169 Overlay Networks for Triton`.

In the body, make sure to include a link to the RFD.

If an RFD is in the `predraft` or `draft` state, you should also [open an
issue](https://code.spearhead.cloud/Spearhead/rfd/issues) to allow for additional
opportunity for discussion of the RFD.  This issue should have the synopsis
that reflects its purpose (e.g. "RFD 169: Discussion") and the body should
explain its intent (e.g. "This issue represents an opportunity for discussion
of RFD 169 while it remains in a pre-published state.").  Moreover, a
`discussion` field should be added to the RFD metadata, with a URL that
points to an issue query for the RFD number.  For example:

```
---
authors: Chewbacca <chewie77@falcon.org>
state: draft
discussion: https://code.spearhead.cloud/Spearhead/rfd/issues?q="RFD+1"
---
```

When the RFD is transitioned into the `publish` state, the discussion issue
should be closed with an explanatory note (e.g. "This RFD has been published
and while additional feedback is welcome, this discussion issue is being
closed."), but the `discussion` link should remain in the RFD metadata.

Note that discussion might happen via more than one means; if discussion is
being duplicated across media, it's up to the author(s) to reflect or otherwise
reconcile discussion in the RFD itself.  (That is, it is the RFD that is
canonical, not necessarily the discussion which may be occurring online,
offline, in person, over chat, or wherever human-to-human interaction can be
found.)

### Finishing up

When discussion has wrapped up and the relevant feedback has been
incorporated, then you should go ahead and change the state of the
document to `publish` and push that change.

### Touching up

As work progresses on a project, it may turn out that our initial ideas
and theories have been disproved or other architectural issues have come
up. In such cases, you should come back and update the RFD to reflect
the final conclusions or, if it's a rather substantial issue, then you
should consider creating a new RFD.

## Contributing

Contributions are welcome, you do not have to be a Spearhead employee to
submit an RFD or to comment on one. The discussions for RFDs happen on
the open on the various mailing lists related to our projects.

To submit a new RFD, please provide a git patch or a pull request that
consists of a single squashed commit and we will incorporate it into the
repository or feel free to send out the document to the mailing list and
as we discuss it, we can work together to pull it into the RFD
repository.
