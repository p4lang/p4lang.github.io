---
layout: page
title: "November 27, 2017"
date: 2017-11-27
author: "Nate Foster"
category: ldwg
---

Attendees: Gordon Brebner (Xilinx), Mihai Budiu (VMware),
Chris Dodd (Barefoot), Andy Fingerhut (Cisco), Andy Keep (Cisco),
James Coole (Cisco), Nate Foster (Cornell), Calin Cascaval (Barefoot),
Matt Massey (Cisco), Joe Tardo (Broadcom)

# Agenda:

* [5 minutes] status and roadmap
  - discussion lead: @gbrebner

* [25 minutes] clarify operations on invalid headers 
  - discussion lead: @jafingerhut
  - GitHub issues: #273 and #285
  - Pull Request: https://github.com/p4lang/p4-spec/pull/450

* [25 minutes] clarify semantics of header stacks
  - discussion lead: @jnfoster
  - GitHub issues: #284
  - Pull Request: https://github.com/p4lang/p4-spec/pull/501

* [25 minutes] proposal for serializable types
  - discussion lead: @akeep
  - GitHub issues: #342
  - Discussion document: https://github.com/akeep/p4-proposals/blob/master/serializable.pdf

* [10 minutes] open


# Status and roadmap

Pick up on selected action items from last meeting.

Plan: Create a P4_14 v1.0.5 maintenance release, and a P4_16 v1.0.1
maintenance release.

Still open for ideas for a P4_18 language.  Gordon Brebner has some
ideas there.



# Clarify operations on invalid headers 

Action items: @jafingerhut

Changes to be made to existing pull request:
- Pull Request: https://github.com/p4lang/p4-spec/pull/450

Add clarification that for fields with enum type, an unspecified value
might not be equal to _any_ of the enum values defined within the enum
declaration.  This may violate compiler assumptions in if-then-else or
select expressions intended to be exhaustive.

Make explicit that reading a header field could be in a header_union
or a header stack, in addition to the already-mentioned header type.

Perhaps: Add one example of a ternary field match in a table with all
bit positions wild-carded, as one way to ignore an unspecified value.



For a header union, specify that invalid header field write must not
change validity of any header_union members.

Remove the last added paragraph.  Add a paragraph near the beginning
of the specification, with wording similar to this:

    "It is understood that some implementations may be unable to
    implement the behavior defined here in all cases.  They should
    document where they deviate from this specification."

No objections to leaving the 'safe behavior' proposed in the pull
request as the default of the language spec.



# Clarify semantics of header stacks

@jnfoster went through the known differences between operations on
header stacks in the P4_14 and P4_16 specification documents, and the
bmv2 simple_switch implementation.

   https://github.com/jafingerhut/p4-guide/blob/master/README-header-stacks.md

@jnfoster had discussed with Antonin Bas before the meeting on this
issue, and Antonin is willing to update bmv2 to whatever the language
working group decides when updating the language specs.

Concerns:

+ We should not change the P4_14 language specification in ways that
  break extant P4_14 programs in significant ways.

+ There should be reasonable ways to auto-translate a P4_14 to P4_16
  program with equivalent behavior.

Proposals:

+ Update P4_14 spec for add_header and remove_header, so they no
  longer have the behavior of 'shifting' existing elements within a
  header stack.  Instead, they will only have an effect on the one
  header stack element that is the argument of the operation.

+ Change bmv2 implementation so that push and pop shift all indices of
  the header stack, not only the elements in range [0, next-1] as it
  does today.

+ In P4_14 and P4_16 language specs, explicitly allow extract() calls
  into header stack elements with constant indexes.  @cdodd: Some
  P4_14 programs use this today.  Such an operation will have no
  effect on the last or next index state maintained in the parser.
  Such an extract() operation could create holes, and is allowed to do
  so.

  + mbudiu - The P4 compiler could warn if the same header stack is
    ever extract'ed into via constant indices in some places, and next
    in other places, warning the user that they are doing this.  It is
    not an error, but since this situation can easily lead to
    confusing behavior, they might not have intended to do so.

+ Keep P4_14 push() operation with behavior of making new pushed
  headers valid, and keep P4_16 push_front() method with behavior of
  making new pushed headers invalid.  Any P4_14 to P4_16 translator
  should translate this in P4_14:

    push(header_stack, N);

  into this in P4_16:

    header_stack.push_front(N);
    header_stack[0].setValid();
    ...
    header_stack[N-1].setValid();

  TBD: whether the translator should also add statements after the
  setValid() calls to initialize all header fields to 0.

mbudiu - would be good to have test cases that cover all of this
behavior.



# Proposal for serializable types

- GitHub issues: #342
- Discussion document: https://github.com/akeep/p4-proposals/blob/master/serializable.pdf

akeep described proposal for serializable types.

What is the goal of a serializable type?

mbudiu - We need to be careful what the goal is here.  For example,
header_union emit would leave out which member header is valid, so you
could not reconstruct the original.

akeep - The same is true of ordinary headers, since validity bit is
not emitted.

Goal of serializable type modifier - could be used as a modifier for
any argument of any control, extern method, parser, etc., meaning that
callers must supply a value with a serializable type for that
argument.

akeep - e.g. Maybe you would want hash functions that require their
argument data to be serializable.

jnfoster - keys to a table are another example that you may want to be
serializable.

akeep - also digest contents.

akeep - Currently emit's restriction on argument types are described
in prose in the language spec.  By introducing 'serializable' types,
we can bring this explicitly into the language itself, and then allow
that type modifier to be used in other places.

mbudiu - I added a comment on Github that we could use P4_16
annotations for this.

akeep - I am not in favor of P4_16 annotations for this purpose,
because in the language spec it is sometimes unclear whether some
annotations are ignorable by an implementation, vs. others that an
implementation must handle.

cdodd - If you want to use serializable for multiple scenarios,
e.g. emit and table keys, are you sure that the same set of things
should be serializable in all of those use cases, or should they be
slightly different sets of objects in different use cases?

akeep - My thinking is that there would be only one format for
serializing these things.

mbudiu - Another approach to this problem is to define extern methods
like serialize_to_bit() or serialize_to_xml(), etc. and they write
data into a buffer somewhere.

akeep - The assumption so far with this 'serializable' keyword is that
we do want to define a wire format for serializable types, and it
should be the same wire format used by different P4 implementations.

The intent is to extend serializable to include:

bit<W> int<W> bool enum, over and above the existing header, header
stack, header_union.  Also, structs nested arbitrarily that "bottom
out" in serializable type.

cdodd - Important to keep the multiple of 8 bit restriction on emit
calls, if emit was generalized to take anything serializable according
to this process.

akeep - For anyone interested in contributing to this proposal or
providing feedback on it, please participate in this public Github
repository:

    https://github.com/akeep/p4-proposals

Proposal: Take the feedback from this discussion, and refine the
current proposal.


# Next meeting

Early January, to keep on monthly schedule.  Possible extra meeting
on 18 December if sufficient progress made on outstanding issues.