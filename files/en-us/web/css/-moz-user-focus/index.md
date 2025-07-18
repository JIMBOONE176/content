---
title: -moz-user-focus
slug: Web/CSS/-moz-user-focus
page-type: css-property
status:
  - deprecated
  - non-standard
browser-compat: css.properties.-moz-user-focus
sidebar: cssref
---

{{deprecated_header}}{{non-standard_header}}

The **`-moz-user-focus`** [CSS](/en-US/docs/Web/CSS) property is used to indicate whether an element can have the focus.

By setting its value to `ignore`, you can disable focusing the element, which means that the user will not be able to activate the element, and the element will be skipped in the tab sequence.
The default is `none`, which disables focussing on the element and removes focus on other elements if there is an attempt to select the element.

## Syntax

```css
/* Keyword values */
-moz-user-focus: none;
-moz-user-focus: normal;
-moz-user-focus: ignore;

/* Global values */
-moz-user-focus: inherit;
-moz-user-focus: initial;
-moz-user-focus: unset;
```

### Values

- `ignore`
  - : The element does not accept keyboard focus and will be skipped in the tab order.
- `normal`
  - : The element can accept keyboard focus.
- `none`
  - : The element does not accept keyboard focus.
    Attempting to select the element removes focus from any other element.

## Formal definition

{{CSSInfo}}

## Formal syntax

{{CSSSyntaxRaw(`-moz-user-focus = ignore | normal | none`)}}

## Examples

### HTML

```html
<input class="ignored" value="The user cannot focus on this element." />
```

### CSS

```css
.ignored {
  -moz-user-focus: ignore;
}
```

## Specifications

Not part of any standard.

## Browser compatibility

{{Compat}}

## See also

- {{cssxref("-moz-user-input")}}
- {{cssxref("user-modify")}}
- {{cssxref("user-select", "-moz-user-select")}}
