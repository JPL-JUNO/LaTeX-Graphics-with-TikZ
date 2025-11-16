# 填充、剪切以及阴影

## 填充区域

- `\fill` 等价于 `\path[fill]`，这不会绘制边框
- `\filldraw` 等价于 `\path[draw,fill]` 以及 `\draw[fill]`，这会绘制边框

## Understanding the path interior

### The nonzero rule

[Figure 7.2 – The inside point and outside point](../07FillingClippingShading/02-inside-outside.pdf)

[Figure 7.3 – The inside point and outside point with a complex path](../07FillingClippingShading/03-inside-outside-complex.pdf)

we choose a ray toward infinity in any direction. Then, we count how many times that ray crosses the path segments, and we consider the direction as shown previously. We will track the number, starting with zero.

This leads us to the following approach:

- If our ray doesn’t cross the path, we have a zero value. Because the path is closed, the ray would have to hit the path if the point is inside. So, zero means that the point is outside.
- Each time when the ray crosses the path, we consider the direction by how it meets the path:
  - If the path goes from the left side to the right side, we add one
  - We subtract one if the path goes from the right side to the left side
- If the final value is zero, the point is outside.
- If the final value is nonzero, the point is inside.

[Figure 7.4 – Filling a path with two parts](../07FillingClippingShading/04-filling-two-parts.pdf)

根据 nonzero rule，可以计算内侧点：0-1-1=-2，对于外侧的点，有 0+1-1+1-1=0，所以整个大三角形区域都是内侧将被填充。

[Figure 7.5 – Reversing a part of the path](../07FillingClippingShading/05-filling-reversed.pdf)

`nonzero rule` can be chosen as an option, such as `\fill[orange, nonzero rule]`, but it’s the default rule, so you don’t need to choose it explicitly.

### The even odd rule

To decide whether a point is inside or outside the path-bordered area, we will consider a ray from that point toward infinity.

This time, the method’s surprisingly simple:

- We count how often the ray crosses the path
- If the total number is even, the point is outside
- If the number is odd, the point is inside

[Figure 7.8 – Nonzero rule on the left and even odd rule on the right](../07FillingClippingShading/08-nonzero-vs-even-odd.pdf)

## Clipping a drawing

Clipping means cutting pieces from a drawing or a path. In other words, it means restricting a picture to a specific area, called the **clipping area** or **clipping path**.

The clipping area is the **interior** of the clipping path.

[Figure 7.15 – A clipped segment of the rings](../07FillingClippingShading/15-clipped-segment.pdf)

## Reverse clipping

[Figure 7.19 – Colored segments of a ring](../07FillingClippingShading/19-colored-segments.pdf)
