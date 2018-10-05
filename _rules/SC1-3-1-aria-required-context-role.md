---
name: ARIA required context role
description: | 
  This rule checks that a role does not exist outside of its required context roles

success_criterion:
- 1.3.1 # Info and Relationships

test_aspects: 
- DOM Tree
- CSS Styling

authors:
- Anne Thyme Nørregaard
---

## Test procedure

### Applicability

The rule applies to any HTML or SVG element that is [exposed to assistive technologies](#exposed-to-assistive-technologies) and has an explicit [semantic role](#semantic-role) with a [WAI-ARIA required context role](https://www.w3.org/TR/wai-aria-1.1/#scope).

### Expectation

Each target element is [owned (per WAI-ARIA)](https://www.w3.org/TR/wai-aria-1.1/#dfn-owned-element) by an element that is [exposed to assistive technologies](#exposed-to-assistive-technologies) and has a [semantic role](#semantic-role) matching one of the [WAI-ARIA required context roles](https://www.w3.org/TR/wai-aria-1.1/#scope).

## Assumptions

_There are currently no assumptions_

## Accessibility Support

This rule relies on assistive technologies to recognize owned elements, as defined by [WAI-ARIA 1.1](https://www.w3.org/TR/wai-aria). This includes when they are nested descendants that are not immediate children. However, some assistive technologies do not recognize owned elements that are not immediate children, unless workarounds are used.

## Background

- [Required Context Role](https://www.w3.org/TR/wai-aria-1.1/#scope)

## Test Cases

### Passed

#### Passed example 1

Element with role ´listitem´ is contained within its required context role ´list´, expressed as an explicit role.

```html
<div role="list">
    <div role="listitem"></div>
</div>
```

#### Passed example 2

Element with role ´listitem´ is contained within its required context role ´list´, through the implicit role of ´ul´.

```html
<ul>
    <div role="listitem"></div>
</ul>
```

#### Passed example 3

Element contained within its required context role even though it is not a direct child of the context role.

```html
<div role="list">
    <div>
         <div>
             <div>
                <div role="listitem"></div>
             </div>
         <div>
    <div>
</div>
```

### Failed

#### Failed example 1

No context role.

```html
<div role="listitem"></div>
```

#### Failed example 2

Wrong context role

```html
<div role="tablist">
    <div role="listitem"></div>
</div>
```

#### Failed example 3

Element not contained within its required context role.

```html
<div role="list"></div>
    <div role="listitem"></div>
```

### Inapplicable

#### Inapplicable example 1

Element does not have an explicit semantic role

```html
<ul></ul>
```

#### Inapplicable example 2

Element is not exposed to assistive technologies.

```html
<div role="tab" aria-hidden="true"></div>
```

#### Inapplicable example 3

Role does not have any required context roles listed in WAI-ARIA spec.

```html
<div role="radio"></div>
```