---
title: <mask>
slug: Web/SVG/Reference/Element/mask
page-type: svg-element
browser-compat: svg.elements.mask
sidebar: svgref
---

The **`<mask>`** [SVG](/en-US/docs/Web/SVG) element defines a mask for compositing the current object into the background. A mask is used/referenced using the {{SVGAttr("mask")}} property and CSS {{cssxref("mask-image")}} property.

## Example

```css hidden
html,
body,
svg {
  height: 100%;
}
```

```html
<svg viewBox="-10 -10 120 120">
  <rect x="-10" y="-10" width="120" height="120" fill="blue" />
  <mask id="myMask" mask-type="luminance">
    <!-- Everything under a white pixel will be visible -->
    <rect x="0" y="0" width="100" height="100" fill="white" />

    <!-- Everything under a black pixel will be invisible -->
    <path
      d="M10,35 A20,20,0,0,1,50,35 A20,20,0,0,1,90,35 Q90,65,50,95 Q10,65,10,35 Z"
      fill="black" />
  </mask>

  <polygon points="-10,110 110,110 110,-10" fill="orange" />

  <!-- with this mask applied, we "punch" a heart shape hole into the circle -->
  <circle cx="50" cy="50" r="50" fill="purple" mask="url(#myMask)" />
</svg>
```

{{EmbedLiveSample('Example', 100, 100)}}

## Attributes

- {{SVGAttr("height")}}
  - : This attribute defines the height of the masking area.
    _Value type_: [**\<length>**](/en-US/docs/Web/SVG/Guides/Content_type#length); _Default value_: `120%`; _Animatable_: **yes**
- {{SVGAttr("mask-type")}}
  - : This attribute defines the mask mode for the contents for the contents of the `<mask>`.
    _Value type_: `alpha` | `luminance`; _Default value_: `luminance`; _Animatable_: **yes**
- {{SVGAttr("maskContentUnits")}}
  - : This attribute defines the coordinate system for the contents of the `<mask>`.
    _Value type_: `userSpaceOnUse` | `objectBoundingBox`; _Default value_: `userSpaceOnUse`; _Animatable_: **yes**
- {{SVGAttr("maskUnits")}}
  - : This attribute defines the coordinate system for attributes {{SVGAttr("x")}}, {{SVGAttr("y")}}, {{SVGAttr("width")}} and {{SVGAttr("height")}} on the `<mask>`.
    _Value type_: `userSpaceOnUse` | `objectBoundingBox`; _Default value_: `objectBoundingBox`; _Animatable_: **yes**
- {{SVGAttr("x")}}
  - : This attribute defines the x-axis coordinate of the top-left corner of the masking area.
    _Value type_: [**\<coordinate>**](/en-US/docs/Web/SVG/Guides/Content_type#coordinate); _Default value_: `-10%`; _Animatable_: **yes**
- {{SVGAttr("y")}}
  - : This attribute defines the y-axis coordinate of the top-left corner of the masking area.
    _Value type_: [**\<coordinate>**](/en-US/docs/Web/SVG/Guides/Content_type#coordinate); _Default value_: `-10%`; _Animatable_: **yes**
- {{SVGAttr("width")}}
  - : This attribute defines the width of the masking area.
    _Value type_: [**\<length>**](/en-US/docs/Web/SVG/Guides/Content_type#length); _Default value_: `120%`; _Animatable_: **yes**

## Usage context

{{svginfo}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- CSS {{cssxref("mask-type")}} property
- Other clipping and masking SVG elements: {{SVGElement("clipPath")}}
- Clipping and masking CSS properties: {{cssxref("mask")}}, {{cssxref("mask-image")}}, {{cssxref("mask-mode")}}, {{cssxref("mask-repeat")}}, {{cssxref("mask-position")}}, {{cssxref("mask-clip")}}, {{cssxref("mask-origin")}}, {{cssxref("mask-composite")}}, {{cssxref("mask-size")}}
