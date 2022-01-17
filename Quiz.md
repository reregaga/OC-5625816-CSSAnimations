[Quiz](https://openclassrooms.com/en/courses/5625816-create-modern-css-animations/exercises/3409)
# Have you built a strong foundation in CSS animations?

## Question 1
**You have a button with a class of .btn, and you want to animate it by increasing its size by 20%, and its background color to change from orange to green when hovered over. Which of the following (written in Sass) would achieve this?**
- [ ] .btn {
  background-color: orange;
  transform: scale(1);
  transition: scale, background-color 600ms;
  &:hover {
    background-color: green;
    transform: scale(1.2);
      
  }
}
- [ ] .btn {
  background-color: orange;
  transform: scale(1);
  transition: all 600ms;
  &:hover {
    background-color: green;
    transform: scale(20%);
      
  }
}
- [ ] .btn {
  background-color: orange;
  transform: scale(1);
  transition: scale 600ms;
  &:hover {
    background-color: green;
    transform: scale(1.2);
      
  }
}
- [x] .btn {
  background-color: orange;
  transform: scale(1);
  transition: all 600ms;
  &:hover {
    background-color: green;
    transform: scale(1.2);
      
  }
}

_If you want to trigger a multi-property transition, using the  all  keyword tells the browser to transition all of the properties you have changed (in this case,  background-color and scale() ) within the :hover pseudo-selector, rather than a specific property.
Also, the parameter of the scale() function should be the desired size as a multiplier of the original size. To increase the size by 20% from the starting scale of 1(100%) we would want to transform to a scale of 1.2(120%)._

## Question 2
**Which of the following are among the essential ingredients for a CSS animation transition?
Careful, there are several correct answers.**
- [x] A property to animate.
- [x] The duration of the transition.
- [ ] The end time of the transition.
- [x] A pseudo-selector to trigger the animation.

_The 4 ingredients to a transition are:

A property to animate.
The before and after values of the property.
The duration of the transition.
A pseudo-selector to trigger the animation.

The end time of the transition is not an ingredient that needs to be given to create a transition._

## Question 3
**Which of the following are among the 12 principles of animation?**
- [x] Staging
- [ ] Primary action
- [x] Timing
- [x] Anticipation

_The 12 principles of animation are:

Squash & stretch
Anticipation
Staging
Straight ahead and pose-to-pose
Follow through and overlapping action
Slow in and slow out
Arc
Secondary Action
Timing
Exaggeration
Solid Drawing
Appeal

Primary action is not one of the principals._

## Question 4
**You want to create an animation where a rocket is launched by clicking a button on the page:

Which of the following HTML and CSS will achieve this?**
- [x] HTML:
&lt;div class="container"&gt;
    &lt;div class="btn"&gt;
      Launch!
    &lt;/div&gt;
    &lt;div class="rocket"&gt;&lt;/div&gt;
&lt;/div&gt;

CSS:
.btn {
  &:active + .rocket{
      transform: translateY(0%);
  }
}

.rocket {
  transform: translateY(100%);
  transition: transform 4s;
}
- [ ] &lt;div class="container"&gt;
    &lt;div class="btn"&gt;
      Launch!
      &lt;div class="rocket"&gt;&lt;/div&gt;
    &lt;/div&gt;
&lt;/div&gt;

.btn:active .rocket{
  transform: translateY(0%);
}

.rocket {
  transform: translateY(100%);
  transition: transform 4s;
}
- [ ] &lt;div class="container"&gt;
    &lt;div class="rocket"&gt;&lt;/div&gt;
    &lt;div class="btn"&gt;
      Launch!
    &lt;/div&gt;
&lt;/div&gt;

.btn {
  &:hover + .rocket{
      transform: translateY(0%);
  }
}

.rocket {
  transform: translateY(100%);
  transition: transform 4s;
}
- [ ] &lt;div class="container"&gt;
    &lt;div class="rocket"&gt;&lt;/div&gt;
    &lt;div class="btn"&gt;
      Launch!
    &lt;/div&gt;
&lt;/div&gt;

.btn {
  &:active + .rocket{
      transform: translateY(0%);
  }
}

.rocket {
  transform: translateY(100%);
  transition: transform 4s;
}

_In this case, you want the :active pseudo-selector to trigger the animation since it is the one activated by clicking the button.
For a pseudo-selector to trigger a transition on another element, that element must be the next sibling in the HTML document. In other words, you must use the adjacent sibling combinator:  +  when setting up the transition. Therefore, the .btn div must be a sibling of the  .rocket div and precede it in the HTML so that the .btn div's :active pseudo-selector can trigger the animation in the  .rocket  div._

## Question 5
**Which is many animators' go-to timing function because of its subtle acceleration and deceleration?**
- [ ] Linear
- [x] Ease-in-out
- [ ] Ease-out-in
- [ ] Ease-out

_The ease-in-out timing function is many animators' go-to because it has subtle acceleration and deceleration curves._

## Question 6
**Which of the following curves represent an ease-in timing function?**
- [ ] 
- [ ] 
- [x] 
- [ ] 

_The ease-in timing function starts with a gentle acceleration curve (it eases in to the movement), and then proceeds at a steady speed until the end of the animation—as represented in answer three._

## Question 7
**Which of the principals of animation does the transition-timing-function CSS property help apply to an element?**
- [ ] Anticipation
- [x] Timing
- [ ] Straight ahead and pose-to-pose
- [x] Slow in and slow out

_The transition-timing-function CSS property sets the acceleration curves for animation transitions by defining the ease-in and ease-out profiles.
As well as implementing the slow in and slow out principal, the ease-in and ease-out profiles are a way of controlling the timing of an element's animation._

## Question 8
**Since the animation in question four does not have the transition-timing-function set, the default acceleration curve is being applied. Which one is the default?**
- [ ] Ease-in
- [x] Ease
- [ ] Ease-in-out
- [ ] Ease-out

_If you don't manually apply a timing function yourself, the browser will apply the ease timing-function._

## Question 9
**You want the rocket launch animation in question four to be more realistic by applying a custom acceleration curve using the  cubic-bezier()  function. You want it to appear to struggle to get off the ground—as it's fighting gravity—when the animation starts. It should then travel at a steady speed upwards when it reaches about halfway up. Like this:

This is what the acceleration curve looks like:

Which of the following functions describes this acceleration curve?
Hint: you can use a tool such as  cubic-bezier.com to find the parameters**
- [ ] cubic-bezier(.65,0,.28,.79)
- [ ] cubic-bezier(0,.65,.28,.79)
- [x] cubic-bezier(.65,0,.79,.28)
- [ ] cubic-bezier(0,.65,.79,.28)

_By using cubic-bezier.com, or any other site or software with "cubic bezier" function generators, you can find the correct parameters for the  cubic-bezier()  function that would generate a desired acceleration curve. 
To create the curve, drag the ease-in and ease-out handles until you've created one that matches the curve in the question, then use the generated cubic-bezier values in your code base._
