---
title: SVGAnimatedNumber
slug: Web/API/SVGAnimatedNumber
page-type: web-api-interface
browser-compat: api.SVGAnimatedNumber
---

{{APIRef("SVG")}}

## SVG animated number interface

The `SVGAnimatedNumber` interface is used for attributes of basic type [\<Number>](/en-US/docs/Web/SVG/Guides/Content_type#number) which can be animated.

### Interface overview

<table class="no-markdown">
  <tbody>
    <tr>
      <th scope="row">Also implement</th>
      <td><em>None</em></td>
    </tr>
    <tr>
      <th scope="row">Methods</th>
      <td><em>None</em></td>
    </tr>
    <tr>
      <th scope="row">Properties</th>
      <td>
        <ul>
          <li>float <code>baseVal</code></li>
          <li>readonly float <code>animVal</code></li>
        </ul>
      </td>
    </tr>
    <tr>
      <th scope="row">Normative document</th>
      <td>
        <a
          href="https://www.w3.org/TR/SVG11/types.html#InterfaceSVGAnimatedNumber"
          >SVG 1.1 (2nd Edition)</a
        >
      </td>
    </tr>
  </tbody>
</table>

## Instance properties

<table class="no-markdown">
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>{{domxref("SVGAnimatedNumber.baseVal")}}</code></td>
      <td>float</td>
      <td>
        The base value of the given attribute before applying any animations.
      </td>
    </tr>
    <tr>
      <td><code>{{domxref("SVGAnimatedNumber.animVal")}}</code></td>
      <td>float</td>
      <td>
        If the given attribute or property is being animated, contains the
        current animated value of the attribute or property. If the given
        attribute or property is not currently being animated, contains the same
        value as <code>baseVal</code>.
      </td>
    </tr>
  </tbody>
</table>

## Instance methods

The `SVGAnimatedNumber` interface do not provide any specific methods.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}
