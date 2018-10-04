---
name: iframe has a unique accessible name

description: |
 Each iframe element has a unique accessible name

success_criterion:
- 4.1.2

test_aspects:
- DOM Tree
- CSS Styling

authors:
- Jey Nandakumar
---

## Test procedure

### Applicability

The rule applies to `iframe` elements that are [exposed to assistive technologies](#exposed-to-assistive-technologies) and have a [non-empty](#non-empty) accessible name.

### Expectation

Each target element has an [accessible name](#accessible-name) that is unique within the [document context](#document-context).

**Note:** 
- `iframes` with the same `src` can have the same [accessible name](#accessible-name).
- Nested `iframe` contents treat the parent `iframe` element as the [document context](#document-context).

## Assumptions

*There are currently no assumptions*

## Accessibility Support

There are no major accessibility support issues known for this rule.

## Background

- [http://www.w3.org/TR/WCAG20-TECHS/H64.html](http://www.w3.org/TR/WCAG20-TECHS/H64.html)
- [https://www.w3.org/TR/2008/REC-WCAG20-20081211/#ensure-compat-rsv](https://www.w3.org/TR/2008/REC-WCAG20-20081211/#ensure-compat-rsv)

## Test cases

### Passed

#### Pass example 1

Usage of `title` attribute to describe the `iframe` content, and there is only one iframe within document context.

```html
<iframe title="List of Contributors" src="../test-assets/SC4-1-2-iframe-unique-name-doc1.html">
</iframe>
```

#### Pass example 2

Multiple `iframe` elements in the document having different `title` descriptions as accessible name.

```html
<iframe title="List of Contributors to Repository 1" src="../test-assets/SC4-1-2-iframe-unique-name-doc1.html">
</iframe>
<iframe title="List of Contributors to Repository 2" src="../test-assets/SC4-1-2-iframe-unique-name-doc2.html">
</iframe>
```

#### Pass example 3

Multiple `iframe` elements in the document having different `aria-label` descriptions as accessible name.

```html
<iframe aria-label="List of Contributors to Repository 1" src="../test-assets/SC4-1-2-iframe-unique-name-doc1.html">
</iframe>
<iframe aria-label="List of Contributors to Repository 2" src="../test-assets/SC4-1-2-iframe-unique-name-doc2.html">
</iframe>
```

#### Pass example 4

Multiple `iframe` elements in the document having different `aria-labelledby` descriptions as accessible name.

```html
<div id="desc-for-title">List of Contributors</div>
<iframe aria-labelledby="desc-for-title" src="../test-assets/SC4-1-2-iframe-unique-name-doc1.html">
</iframe>
<div id="desc-for-title1">List of Reviewers</div>
<iframe aria-labelledby="desc-for-title1" src="../test-assets/SC4-1-2-iframe-unique-name-doc2.html">
</iframe>
```

#### Pass example 5

`iframes` having the same `title` within a given document context, but one of them is not exposed to assistive technologies.

```html
<iframe style="display:none;" title="List of Contributors" src="../test-assets/SC4-1-2-iframe-unique-name-doc1.html">
</iframe>
<iframe title="List of Contributors" src="../test-assets/SC4-1-2-iframe-unique-name-doc2.html">
</iframe>
```


#### Pass example 6

`iframes` are allowed to have the same `title` across different document contexts. In this example `iframe` with `id` `level2-frame1` has a parent document context of `iframe` with `id` `level1-frame2`, and does not share the document context of `iframe` with `id` `level1-frame1`.

```html
<iframe id="level1-frame1" title="List of Contributors" src="../test-assets/SC4-1-2-iframe-unique-name-doc1.html">
</iframe>
<iframe id="level1-frame2" title="List of Contributors 2" src="../test-assets/SC4-1-2-iframe-unique-name-doc2.html">
  <iframe id="level2-frame1" title="List of Contributors" src="../test-assets/SC4-1-2-iframe-unique-name-doc1.html">
  </iframe>
</iframe>
```

### Failed

#### Fail example 1

Multiple frames having the same `title` within a given document context.

```html
<iframe title="List of Contributors" src="../test-assets/SC4-1-2-iframe-unique-name-doc1.html">
</iframe>
<iframe title="List of Contributors" src="../test-assets/SC4-1-2-iframe-unique-name-doc2.html">
</iframe>
```

#### Fail example 2

Multiple frames having the same `aria-label` within a given document context.

```html
<iframe aria-label="List of Contributors" src="../test-assets/SC4-1-2-iframe-unique-name-doc1.html">
</iframe>
<iframe aria-label="List of Contributors" src="../test-assets/SC4-1-2-iframe-unique-name-doc2.html">
</iframe>
```

#### Fail example 3

Multiple frames having the same name given by `title` and `aria-label` within a given document context

```html
<iframe title="List of Contributors" src="../test-assets/SC4-1-2-iframe-unique-name-doc1.html">
</iframe>
<iframe aria-label="List of Contributors" src="../test-assets/SC4-1-2-iframe-unique-name-doc2.html">
</iframe>
```

### Inapplicable

#### Inapplicable example 1

Accessible name provided is empty.

```html
<iframe title="" src="../test-assets/SC4-1-2-iframe-unique-name-doc1.html">
</iframe>
<iframe aria-label="" src="../test-assets/SC4-1-2-iframe-unique-name-doc3.html">
</iframe>
```

#### Inapplicable example 2

Usage of `alt` attribute to describe content is not valid.

```html
<iframe alt="Some" src="../test-assets/SC4-1-2-iframe-unique-name-doc1.html">
</iframe>
```

#### Inapplicable example 3

Does not apply to non `iframe` elements.

```html
<object title="List of Contributors" src="../test-assets/SC4-1-2-iframe-unique-name-doc1.html">
</object>
<object aria-label="List of Contributors Clone" src="../test-assets/SC4-1-2-iframe-unique-name-doc3.html">
</object>
```

#### Inapplicable example 4

No accessible name is provided

```html
<iframe src="../test-assets/SC4-1-2-iframe-unique-name-doc1.html">
</iframe>
<iframe src="../test-assets/SC4-1-2-iframe-unique-name-doc3.html">
</iframe>
```

#### Inapplicable example 5

Does not apply to `iframe` elements that are not exposed to assistive technologies.

```html
<iframe style="display:none;" title="Document One" src="../test-assets/SC4-1-2-iframe-unique-name-doc1.html">
</iframe>
<iframe style="display:none;" aria-label="Document One" src="../test-assets/SC4-1-2-iframe-unique-name-doc3.html">
</iframe>
```