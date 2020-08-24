---
title: Template as a function
status: DRAFTED
created_at: 2020-08-24
updated_at: 2020-08-24
pr: (leave this empty until the PR is created)
---

# Template as a function

## Summary

Template as a function allows to define a function that returns a template class instance that then can be processed by LWC engine to generate output instead of using static templates.

## Basic example

```javascript
import tpl from '(tbd)';

class InputComponent extends LightningElement {
  render() {
    return tpl`
    ${this.labelTemplate()}
    <div class="container">
      ${this.inputTemplate()}
      ${this.inputTemplate()}
      ${this.inputTemplate()}
    </div>
    `;
  }

  labelTemplate() {
    return tpl`<slot name="label"></slot>`;
  }

  inputTemplate() {
    return tpl`
    <input
      name="${this.name}"
      value="${this.value}"
    />
    `;
  }

  prefixTemplate() {
    return tpl`<slot name="prefix"></slot>`;
  }

  suffixTemplate() {
    return tpl`<slot name="suffix"></slot>`;
  }
}

```

## Motivation

LWC today does not encourage reusability of assets already created in a components ecosystem.
To gain scale when developing base components for a components ecosystem (or any library of components) reusability is a basic requirement.


Why are we doing this? What use cases does it support? What is the expected
outcome?

Please focus on explaining the motivation so that if this RFC is not accepted,
the motivation could be used to develop alternative solutions. In other words,
enumerate the constraints you are trying to solve without coupling them too
closely to the solution you have in mind.

## Detailed design

This is the bulk of the RFC. Explain the design in enough detail for somebody
familiar with Lightning Web Components to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here.

## Drawbacks

Why should we *not* do this? Please consider:

- implementation cost, both in term of code size and complexity
- whether the proposed feature can be implemented in user space
- the impact on teaching people Lightning Web Components
- integration of this feature with other existing and planned features
- cost of migrating existing Lightning Web Components applications (is it a breaking change?)

There are tradeoffs to choosing any path. Attempt to identify them here.

## Alternatives

What other designs have been considered? What is the impact of not doing this?

## Adoption strategy

If we implement this proposal, how will existing Lightning Web Components developers adopt it? Is
this a breaking change? Can we write a codemod? Should we coordinate with
other projects or libraries?

# How we teach this

What names and terminology work best for these concepts and why? How is this
idea best presented? As a continuation of existing Lightning Web Components patterns?

Would the acceptance of this proposal mean the Lightning Web Components documentation must be
re-organized or altered? Does it change how Lightning Web Components is taught to new developers
at any level?

How should this feature be taught to existing Lightning Web Components developers?

# Unresolved questions

Optional, but suggested for first drafts. What parts of the design are still
TBD?
