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

The key to build a scalable ecosystem of web components is reusability of assets already created. Scalable front-end includes multiple items like composition (parent-child), extensibility (class extension), and reuse of a template. Today LWC does not allow to build reusable templates which leads to a situation where when creating a set of components they can't reuse already defined assets (the templates).

Consider the following scenario.

An author builds a set of base components for their organization. It includes all kind of inputs, lists, dropdowns, alerts, etc. Then the author builds a higher-level composite component like a chip input that would use a template defined for the input and add a template to render "chips". (See an example [here](https://awc.dev/chip-input)).

In other cases, an author may want to change a template of the superclass to modify an element to fit a new use case. In such a situation they only override a template function responsible for producing a template for a specific part of the UI of the component.

Another use case is when building a UI for several components that have similar functionality. A real-life example for the domain modelling project is an excellent illustration of this use case. This project has several similar forms. Each form has common items like name and description. Instead of copying the same template into each form, instead, the preferred way is to use a function that the author calls to return the form element (including parametrization like a label or a hint text via arguments).

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
