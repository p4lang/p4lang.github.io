---
layout: code
title: Community Projects
permalink: code/projects.html
description: "Projects for developers"
---

# Language projects

### Allow compile time constants into expressions

Github issues: [294](https://github.com/p4lang/p4-spec/issues/294),
[331](https://github.com/p4lang/p4-spec/issues/331).

### Initialization of header stacks and structs

Github issues: [198](https://github.com/p4lang/p4-spec/issues/198),
[341](https://github.com/p4lang/p4-spec/issues/341).

### P4<sub>16</sub> formal semantics

- - -

# Compiler projects

### Preprocessor

Streamline preprocessing of P4. Currently the compiler needs to invoke
cpp even when invoked with --no-cpp because it needs the
preprocessor to inline #include files. And moreover, it is using a
hardcoded system include path because the compiler options are not
passed to the method invoking the preprocessor. This can turn into a
significant improvement in execution time if cpp is not spawned as a
process for every include directive.

### p4c compiler driver

Streamline the mechanism of the compiler driver to pass options to the
backend. Even though we have the -Xp4c option, developers expect
that the driver supports all the backend options natively. We have
been adding a number of these directly into the driver, however, that
is not a scalable solution.

### Compiler error reporting

Improve compiler [error reporting](https://github.com/cc10512/p4c/blob/cc/errorhandling/docs/doxygen/03_errorhandling.md)

### IR Tools

Implemente the analog of P4<sub>14</sub> p4-graphs that works
with the p4c IR.


### Documentation

Fully document the classes for both IR and compiler passes and
organize the documentation into chapters. There is also significant
material captured in a Powerpoint presentation that would be good to
integrate into the generated HTML documentation.

- - -

# Modeling projects

### Implement PSA on the behavioral model. Details soon.

- - -

# Infrastructure projects

### Details to follow.
