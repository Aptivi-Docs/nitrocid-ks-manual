---
description: Your random number generator is here! Let's see if you're lucky.
icon: slot-machine
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/inner-workings/inner-essentials/random-number-generation
---

# Random Number Generation

The random number generator is a module that allows you to get a random number from the smallest possible number to the largest possible number. It's available for the majority of the computers, such as your desktop computer, your tablet, and so on.

Random number generation involves a sequence of numbers that can't be reasonly predicted by a human in which a random number in the sequence is selected. For example, a dice is an example of a mechanical hardware RNG. You can read more about random number generation [here](https://en.m.wikipedia.org/wiki/Random_number_generation).

***

## <mark style="color:$primary;">Random number generation in Nitrocid</mark>

Nitrocid has a random number generator driver that allows you to generate various random numbers or choices based on your purpose, such as getting a random integer number, a random boolean (true or false), and so on.

<details>

<summary>Random Numbers</summary>

When it comes to RNGs, the most essential task for such operation is to generate a random integer number within a sequence. You can easily access such operations using the `RandomDriver` class, which wraps around the current random number generator driver that you can set up.

You have various types of random number generation classes, such as:

<table><thead><tr><th width="209.6666259765625">Function</th><th>Description</th></tr></thead><tbody><tr><td><code>Random()</code></td><td>Gets a random number from 0 to the maximum integer value, inclusive.</td></tr><tr><td><code>Random(max)</code></td><td>Gets a random number from 0 to the specified number, inclusive.</td></tr><tr><td><code>Random(min, max)</code></td><td>Gets a random number from the minimum number, inclusive, to the specified maximum number, inclusive.</td></tr><tr><td><code>RandomShort()</code></td><td>Gets a random number from 0 to the maximum short integer value, inclusive.</td></tr><tr><td><code>RandomShort(max)</code></td><td>Gets a random number from 0 to the specified number, inclusive.</td></tr><tr><td><code>RandomShort(min, max)</code></td><td>Gets a random number from the minimum number, inclusive, to the specified maximum number, inclusive.</td></tr><tr><td><code>RandomIdx()</code></td><td>Gets a random number from 0 to the maximum integer value, exclusive.</td></tr><tr><td><code>RandomIdx(max)</code></td><td>Gets a random number from 0 to the specified number, exclusive.</td></tr><tr><td><code>RandomIdx(min, max)</code></td><td>Gets a random number from the minimum number, inclusive, to the specified maximum number, exclusive.</td></tr><tr><td><code>RandomDouble()</code></td><td>Gets a random floating-point number from 0 to a value that is less than 1.0.</td></tr><tr><td><code>RandomDouble(max)</code></td><td>Gets a random floating-point number from 0 to the specified number, exclusive.</td></tr></tbody></table>

</details>

<details>

<summary>Random Boolean Decisions</summary>

When it comes to random boolean decisions, you have various types to generate a random boolean decision:

<table><thead><tr><th width="226.33331298828125">Function</th><th>Description</th></tr></thead><tbody><tr><td><code>RandomChance(prob)</code></td><td>Gets a random boolean answer from the probability by a raw value from 0.0 (0%) to 1.0 (100%).</td></tr><tr><td><code>RandomChance(percent)</code></td><td>Gets a random boolean answer from the probability by a percentage value from 0% (0.0) to 100% (1.0).</td></tr><tr><td><code>RandomRussianRoulette()</code></td><td>Gets a random boolean value based on a Russian Roulette luck factor.</td></tr><tr><td><code>RandomBoolean()</code></td><td>Gets a random boolean value based on a normal random number generation.</td></tr></tbody></table>

</details>

This is all wrapped with a kernel driver handler, which you can read about it below:

{% content-ref url="kernel-drivers/" %}
[kernel-drivers](kernel-drivers/)
{% endcontent-ref %}
