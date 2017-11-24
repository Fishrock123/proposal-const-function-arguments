# ECMAScript Const Function Arguments

This proposal introduces constant function argument references, which allows for better enforcement of explicit variable mutability.

## Status

**Stage:** 0  
**Champion:** tbd

_For more information see the [TC39 proposal process](https://tc39.github.io/process-document/)._

## Authors

* Jeremiah Senkpiel (@fishrock123)

# Proposal

When declaring a function or an arrow function, adding `const` before the argument declaration makes the argument reference immutable, in the same manner as if the argument was a variable declared by the `const` variable declaration keyword. Just like `const` variables, the immutability is only by reference for objects, and does not extend deeply.

```
function (const a) {
  const b

  // a is immutable in the same way b is
}
```

```
(const a) => {
  const b

  // a is immutable in the same way b is
}
```

## Interaction with default arguments

Default arguments still function as normal. The immutability happens once the function body begins, and default argument statements are treated as the declaration assignment.

```
function (const a = 'hello') {
  const b

  // a is immutable in the same way b is
  // if `a` was not passed to the function, `a` will be 'hello'
}
```

## Interaction with the `arguments` object

Constant function argument make the direct argument references immutable. This does not impact the `arguments` object, in strict or sloppy mode, which hold its own references and may be mutated as normal.

In sloppy mode, assigning to the arguments object will not update a constant function argument.

## "What about `let` and `var`?"

This proposal only touches what is currently missing. Neither `let` or `var` are necessary as that is already the default behavior.

# Open Questions

Would it be possible to use const function arguments in an arrow function that has just one argument and no parentheses?

```
const myFunc = const a => {
  const b

  // a is immutable in the same way b is
}
```

## Potential short-hand options

Is a short-hand version desirable? What could be used that is still clear on its purpose?

# Grammar

TODO

```grammarkdown
```

# Resources

TODO?

# TODO

The following is a high-level list of tasks to progress through each stage of the [TC39 proposal process](https://tc39.github.io/process-document/):

### Stage 1 Entrance Criteria

* [ ] Identified a "[champion][Champion]" who will advance the addition.  
* [x] [Prose][Prose] outlining the problem or need and the general shape of a solution.  
* [ ] Illustrative [examples][Examples] of usage.  
* [ ] ~High-level API~ _(proposal does not introduce an API)_.  

### Stage 2 Entrance Criteria

* [ ] [Initial specification text][Specification].  
* [ ] _Optional_. [Transpiler support][Transpiler].  

### Stage 3 Entrance Criteria

* [ ] [Complete specification text][Specification].  
* [ ] Designated reviewers have [signed off][Stage3ReviewerSignOff] on the current spec text.  
* [ ] The ECMAScript editor has [signed off][Stage3EditorSignOff] on the current spec text.  

### Stage 4 Entrance Criteria

* [ ] [Test262](https://github.com/tc39/test262) acceptance tests have been written for mainline usage scenarios and [merged][Test262PullRequest].  
* [ ] Two compatible implementations which pass the acceptance tests: [\[1\]][Implementation1], [\[2\]][Implementation2].  
* [ ] A [pull request][Ecma262PullRequest] has been sent to tc39/ecma262 with the integrated spec text.  
* [ ] The ECMAScript editor has signed off on the [pull request][Ecma262PullRequest].  

# Misc

Proposal formatting taken from [rbuckton's proposal-shorthand-improvements](https://github.com/rbuckton/proposal-shorthand-improvements).

<!-- The following are shared links used throughout the README: -->

[Champion]: #status
[Prose]: #proposal
[Examples]: #proposal
[Specification]: #todo
[Transpiler]: #todo
[Stage3ReviewerSignOff]: #todo
[Stage3EditorSignOff]: #todo
[Test262PullRequest]: #todo
[Implementation1]: #todo
[Implementation2]: #todo
[Ecma262PullRequest]: #todo
