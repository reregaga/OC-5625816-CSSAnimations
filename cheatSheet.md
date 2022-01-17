To **create animations with CSS**, you use either **transitions** or **keyframes**. While **keyframes require a bit more** to get set up and running, transitions only require a few bits of info to create. They are perfect for quick, simple animations, such as changing the appearance of a button when the user hovers over it.

## Transitions
Transitions allow **change the value of a property over a set amount of time**. The **startpoint is the initial value** of the animated property, the **endpoint is its final value**, and the **time to complete is its duration**, and **trigger**. 
```html
<style>
.btn {
    transform: scale(1); /*startpoint*/
    transition-property: transform; /*for duration*/
    transition-duration: 400ms; /*for duration*/
}
.btn:hover { transform: scale(1.15); } /*endpoint, destination, hover is trigger*/
</style>
<div class="btn">Look Ma! I'm growing!</div>
```
Shorthand:
```css
.btn {
    transform: scale(1); /*startpoint*/
    transition: transform 400ms; /*for duration*/
}
.btn:hover { transform: scale(1.15); } /*endpoint, destination, hover is trigger*/
```

## Pseudo-classes
[50 pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)

A pseudo-class is a lot like an if-statement for the browser: **If the condition of the pseudo-class is true, then apply its styling to the object**.

Following are pseudo-classes **commonly used** in conjunction with transitions:
- `:hover`
- `:active`
- `:focus`
- `:valid`
- `:invalid`
- `:not()`
- `:checked`
- `:enabled`
- `:disabled`

[HTML5 validate fields](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms/Form_validation)
```html
<style>
.form__group input {
    border: 2px solid yellow;
    outline: none;
}
.form__group input:focus { border: 2px solid green; }
.form__group input:invalid { background: red; border: 2px solid red; } 
</style>
<div class="form">
    <div class="form__group">
        <label for="">email</label>
        <input type="email" name="" id="">
    </div>
</div>
```
It's validating the email address as it's being entered, but flickering between the `:focus` and `:invalid` is a bit obnoxious. Let's make use of the `:not()` pseudo-selector, combined with the `:focus` pseudo-selector to allow the user to finish entering their email address before telling them whether it's valid or not. The `:not()` pseudo-selector registers as `true` when it's containing selector registers as `false`.
```css
.form__group input:focus { border: 2px solid green; }
.form__group input:not(:focus):invalid { background: red; border: 2px solid red; }
```
In this case, `:not()` will return `true` if the `input` is **not** in the `:focus` state. You can **chain pseudo-classes together**, just like with standard classes. In this case, we've created a pseudo-selector that will apply its rule set if the element isn't in the `:focus` state **and** the email address is `:invalid`. 

Let's add animation to the changes in state by adding a transition for the  `background-color`.
```css
.form__group input {
    border: 2px solid yellow;
    outline: none;
    transition: background-color 500ms; /* ! */
}
```

![Fig 1](img/fig_1.gif)

### Trigger transition on another element
For a pseudo-selector to **trigger a transition on another element**, that element **must be the next sibling** in the HTML document. In other words, you must use the adjacent sibling combinator:  `+`  when setting up the transition.

```html
<style>
.btn:hover + .ball{
    transform: scale(1.5);
}
.ball { width: 20px; height: 20px; }
</style>

<div class="container">
    <div class="btn">Grow!</div>
    <div class="ball"></div>
</div>
```
Now when you hover over the button, `.ball` will scale up **instead** `.btn`.

Let's change things up a bit, and, rather than starting huge and getting huger, let's have it start small by setting the initial `scale()` to `.1`, and add a transition.
```css
.btn:hover + .ball{
    transform: scale(1.5);
}
.ball {
    transform: scale(0.1);
    transition: transform 4000ms;
}
```
Finally, let's change the `:hover` selector to `:active`, so **the scale increases when the button is pressed**, rather than simply hovered over.
```css
.btn:active + .ball{
    transform: scale(1.5);
}
.ball {
    transform: scale(0.1);
    transition: transform 4000ms;
}
```

### The 12 principles of animation:
[Wikipedia](https://en.wikipedia.org/wiki/Twelve_basic_principles_of_animation)
- Squash and stretch
- Anticipation
- Staging
- Straight ahead and pose-to-pose
- Follow through and overlapping action
- Slow in and slow out
- Arc
- Secondary action
- Timing
- Exaggeration
- Solid drawing
- Appeal

### Combine transitions:
Previously, we built a button that grows when hovered over. It's built as a `<div>` with the class of  `.btn` assigned to it:
```scss
.btn {
    background-color: red;
    transition: transform 450ms;
    &:hover {
        transform: scale(1.2);
    }
}
```
Let’s spice up the button a bit and layer in some **secondary animation** by creating a `:hover` state that fades in the `background` as the button expands. There's a few ways to go about animating opacity, and we'll talk about a more performant (but complex) solution in a bit. But for the sake of simplicity, let's transition the `background-color`  between two different `rgba()` values. 
```scss
$cd-btn-start: rgba(1, 28, 55, 0);
$cd-btn-end: rgba(1, 28, 55, 1);
```
They both have the same RGB values, but `$cd-btn-start` has an alpha value of `0`, making it **transparent**, whereas `$cd-btn-end` has an alpha value of `1`, making it **opaque**. Now, to add a transition for our opacity change, we need to add new color variables to the `.btn`  selector and its `:hover` state:
```scss
.btn {
    background-color: $cd-btn-start;
    &:hover {
        transform: scale(1.2);
        background-color: $cd-btn-end;
    }
}
```
When you want to **transition multiple properties at once**, rather than typing the name of the property that you want to transition: `transition: transform 450ms;`. Instead use the `all` keyword in its place:
```css
transition: all 450ms;
```
By using the `all` keyword, you are telling the browser to **transition all of the properties you have changed**.
```scss
.btn {
    background-color: $cd-btn-start;
    transition: all 450ms;
    &:hover {
        transform: scale(1.2);
        background-color: $cd-btn-end;
    }
}
```

![Fig 2](img/fig_2.gif)

Using the `all` keyword is perfect for when you want **multiple things to happen at the same time, and for the same duration**, but there's **another way** to add multiple properties to a transition.  Rather than using all, you can **list out the animations for each property** that you'd like to transition, separated by commas.
```css
transition: transform 450ms, background-color 300ms; /* transitions for transform and background-color */
```
Now that they're separate, you can **give them different durations**. Now the `background-color` will be fully opaque before the button has finished scaling up.

### Delaying transitions:
Right now we are transitioning two properties, with two separate durations, but **both begin simultaneously**. What would be nice is if the `background-color` transition **waited 150ms before starting** so that they both finish their animations at the same time. 

We need to use the `transition-delay` property:
```css
transition-delay: 150ms;
```
Since there are two transitions occurring, you need to **specify a value for each, in the order that they are declared** in the `transition` property: 
```css
transition: transform 450ms, background-color 300ms;
transition-delay: 0, 150ms;
```
But, just like  `transition-property` and `transition-duration`, you can write the same thing more concisely by adding `transition-delay` values to the `transition` property itself, after the  `transition-duration` values:
```css
transition: transform 450ms, background-color 300ms 150ms;
```
In the case of an absence for a delay value, the `transition` property will assume a zero delay, so you can omit it in `transform`.
```scss
.btn {
    background-color: $cd-btn-start;
    transition: transform 450ms, background-color 300ms 150ms;
    &:hover {
        transform: scale(1.2);
        background-color: $cd-btn-end;
    }
}
```
### Timing functions:
Every object that has ever moved and ever will move does two specific things. To begin moving, they have to **accelerate**, and before they can stop, they have to **decelerate**. If you want your animations to **feel grounded and authentic**, then it’s vital that you pay attention to how objects accelerate and decelerate, or, in animation terminology, how they **ease in** and **ease out**.

The X-axis represents the percentage of the duration completed, and the Y-axis represents the percentage of the motion completed. Start at 0% duration and 0% progress in the lower left corner, and finish in the upper right corner, where both the progress and durations have reached 100%. 

![Fig 3](img/fig_3.jpg)

Notice that the **velocity isn't a straight line**. Instead, its slope changes as the box accelerates at the beginning and decelerates at the end. In the beginning, the box isn't moving very quickly yet, so it hasn't completed as much progress as it has duration, making the line flatter.

 In CSS, these **acceleration curves** are called **timing functions**, and you can use the  `transition-timing-function`  property to set the acceleration curves for your transitions.
 
 **CSS comes preloaded with a variety of its own curves** right at your fingertips. Let's begin with the curve that wasn't. 
 - `linear` timing function has no acceleration or deceleration to its velocity.
 ```css
transition: transform 1000ms;
transition-timing-function: linear;
```
... or Shorthand:
```css
transition: transform 1000ms linear;
```
- `ease-in-out` speed ramping up and down, but it's subtle enough to sort of disappear into the motion. In other words, it looks and feels natural. 
```css
transition: transform 1000ms ease-in-out;
```
You also have the option to just **ease in**, or **ease out** of motion with the `ease-in` and `ease-out` keywords.
```css
/* ease-in timing-function: */
transition: transform 1000ms ease-in;

/* ease-out timing-function: */
transition: transform 1000ms ease-out;
```
`ease-in` graph is essentially **the start of the `ease-in-out` graph, with a `linear` ending**. And `ease-out` is just the opposite, with a `linear` start and `ease-in-out`'s deceleration curve.

 **If you don't manually choose one, the browser will apply the `ease` timing function**, which sounds a lot like the other curves we've just covered. However, it has its own distinct profile, featuring a sharper acceleration profile, while the deceleration ramp is more pronounced.
 
 #### Own functions
 CSS' built-in timing functions are really just shorthand for `cubic-bezier` functions. 
 ```css
.selector {
    transition-timing-function: cubic-bezier(.42, 0, .58, 1);
}
```
`cubic-bezier()` **requires a list of four numbers** as arguments, which are actually the **coordinates for two points** that live on the plane of the graph. The first two numbers are the X and Y coordinates for the point that determines the ease in of the acceleration curves, and the second pair determines its ease out
```css
.selector {
                                            /*(X1,Y1)(X2,Y2)*/
    transition-timing-function: cubic-bezier(.42, 0, .58, 1);
}
```

![Fig 4](img/fig_4.jpg)

**Online tool to help build** it, such as [cubic-bezier.com](https://cubic-bezier.com/#.17,.67,.83,.67).
