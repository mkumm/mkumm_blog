+++
title = 'Math Speak Primer'
date = 2024-05-14T07:19:44+02:00
tags = ['math', 'symbols', 'primer']
draft = true
summary = "An ongoing and often updated reference for current and future posts. Last updated 2024-05-14"
+++
{{< katex >}}

{{<lead>}}
A growing reference to support current and upcoming posts.
{{</lead>}}

_Last updated 2024-05-14"_



## Quick Reference of Common Symbols

{{% columns %}}

{{% column %}}
| Symbol | English |
|--------|---------|
| \\( \in \\)   | "is an element of" |
| {}       | "the set of" |
| : | "such that" |
| \\( \wedge \\) | "and" |
| \\( \vee \\) | "or" |
| \\( \Rightarrow \\) | "implies" |
| \\( \forall \\) | "for all" |


{{% column %}}
| Symbol | English |
|--------|---------|
| \\( \exists \\) | "exists" |
| \\( \neg \\) | "not" |
| \\( \N \\)   | Natural numbers (maybe 0) |
| \\( \R \\)      | Real numbers |
| \\( \Complex \\)      | Complex numbers |
| \\( \phi \\) or _dom_ | "in our domain" |

{{% endcolumns %}}



## Sets

We developers, whether consciously or not are mostly thinking in sets. Sometimes our sets are rather generic like `numbers` or `characters`. Sometimes we even have well defined sets like `u8` _unsigned 8-bit integer_ which in math speak could be defined as  $\{0, 1, 2,..., 255\}$ or $\{x : x  \geqq 0\ and\ x \leqq 255\}$ which in english is "The set of x such that x is greater than or equal to 0 and x is less than of equal to 255"

## Functions Really...

When working with functions, in the strictist sense, we have to consider both the **domain** of the _things_ we are starting with and the **domain** or **range** of _things_ that our functions return. The more generic our domains and ranges, the more generic our function is. Generic may not be a bad thing in this case.

### TS examples
