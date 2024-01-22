## What I have created

---

- I have created a black hole loading screen, this code creates a circular gradient loader animation with a blur effect.
- The loader's continuous rotation and blur imply ongoing background activity, commonly used as a visual cue for loading or processing states in web applications. The design is minimal yet visually engaging, drawing the user's attention while they wait.

---

## Feedback, general ideas to improve work

### EXTRA NOTES AND PIECES 
```html
<div classs = loader>
	<span></span>
	<span></span>
	<span></span>
	<span></span>
</div>
```

This is the main container for the the loader animation, the four spans act as layered circular elements within the element.

### CSS STYLING SECTION

```css
body {
/*FILLS THE ENTIRE PAGE*/
  width: 100vw;
  height: 100vh;
/*makes it so the layout is consistent and at a default at 0*/
  margin: 0;
  padding: 0;
/*creates the dark colour back-drop behind the loader */
  background-color: #141416;
/*centers the loader into the middle */
  display: flex;
  justify-content: center;
  align-items: center;
}
```

---

```css
.loader {
/* When you set position: relative; on an element, it creates a positioning context for its children, but the element itself stays in the normal flow of the document.*/
  position: relative;
/* size and width of the initial container */
  height: 100px;
  width: 100px;
/* creates a circular shape instead of the typical box container */
  border-radius: 50%;
/*gradient colour that goes from left to right with those colors */
  background: linear-gradient(
    90deg,
    rgba(36, 14, 0, 1) 0%,
    rgba(121, 9, 100, 1) 47%,
    rgba(218, 0, 255, 1) 100%
  );
/* create space above and below the loader in the centered layout. */
  margin-top: 100px;
  margin-bottom: 100px;
```

A relatively positioned circular container with a background gradient as the base layer of the loader. It's animated to rotate 360 degrees continuously, creating the spinning effect.
Margins are added to ensure it's vertically centered with space around.

---

```css
.loader span {
  position: absolute;
  width: 100%;
  height: 100%;
  border-radius: 50%;
  background: linear-gradient(77.28deg, rgba(82, 225, 226, 1)2.24%, rgb(109, 77, 196) 104.45%);
/* use this to change and speed up the animation of the loader as it rotates oveover inifinitely */
  animation: animate 0.5s linear infinite;
}

/* EACH LAYER IS POSITIONED ON TOP OF THE BASE LAYER 
Child elements (*span*) are absolutely positioned inside the loader, taking up the full width and height.Each span has a border-radius, background gradient, and the same spinning animation (animate) for a consistent effect.
nth-child selectors apply different blur effects to each span, creating a layered appearance. */

.loader span:nth-child(1) {
  filter: blur(5px);
}

.loader span:nth-child(2) {
  filter: blur(10px);
}

.loader span:nth-child(3) {
  filter: blur(25px);
}

.loader span:nth-child(4) {
  filter: blur(50px);
}
```

Absolutely `positioned` to cover the entire **`.loader`**container, creating multiple layers over the base layer. Each `span` is identical to the `loader` in size and background but with varying levels of blur applied, creating a diffused light effect.

---

```css
.loader::after {
/*The content property is  always sued with psuedo-elements, *in this instance (after) to insert content an element.* When used with the ::after pseudo-element, it's typically used for decorative or stylistic purposes. */
    content: '';
/* Positions the pseudo-element relative to the .loader element.*/
    position: absolute;
/* pairing this with the *position above, content border above is set a 3-pixel distance from the edges of the border, effectively crating a circular border around it.**/
    top: 3px;
    left: 3px;
    right: 3px;
    bottom: 3px;
/*choosing the color of the content property that is on top, keeping it black gives the visual effect of a black hole and the border radius keep it the same shape as the base layer  */
    background-color: #141416;
    border-radius: 50%;
  }
/* the rotation progresses smoothly from 0 to 360 degrees without intermediate steps, resulting in a continuous and even rotation.*/
  @keyframes animate {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
```

- An additional pseudo-element (**`::after`**) is created to add a border around the loader, enhancing its appearance.

The choice of **`position: relative;`** for the loader element allows child elements (**`span`** and **`::after`**) positioned using **`position: absolute;`** to be positioned relative to the **`.loader`** container. This is especially relevant when using absolute positioning and ensures that child elements are positioned relative to the loader itself rather than the entire viewport.
