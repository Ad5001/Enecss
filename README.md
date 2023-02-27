# enecss
(or backwards, sscene)

A CSS library to facilitate the creation of low-poly 3D scenes using only CSS.
---

## Building

Use [Sass](https://sass-lang.com/) to build enecss...
```bash
sass src/main.scss main.css
```
...or include it into your own builds.
```sass
@import "enecss/src/main.scss";
```

## Using

### Creating the scene

Once you've included enecss into your HTML file, you can declare a scene and a root node in HTML using the following:
```html
<section class="scene">
    <figure class="root" style='--width: 400px; --height: 400px;'>
    </figure>
</section>
```

The 2D size of the scene is provided in the `--width` and `--height` variables. The default depth is `600px`, and is currently hardcoded.

**Note**: This guide will make extensive use of inline styling for ease of use and easy representability. If your context does not allow you to use this tool, you can just declare an ID to every node and port those styles to a stylesheet.
**Note**: A `section` is not mandatory for the scene node. However, the `figure` node is necessary for every object element you want to create.

### Creating objects

There are a few basic objects. All parameters of the objects will be specified in CSS variables (which, as mentioned previously, can be set either inline or via a stylesheet).

1. The basic mesh

This is the most basic element in the list, a rectangle. It doesn't even need to be a `figure`, and can take a single texture, which will be reproduced on both its sides.

Example: A white rectangle with a black outline.
```html
<div style="width: 500px; height: 500px; background: white; outline: solid 1px black;"></div>
```

Other objects are often composed of basic meshes, to which you can style and use like any other HTML element (See [Manipulating meshes](#Manipulating-meshes))

2. Axises

Object transformations are relative to their own position and rotation. If you're having trouble figuring out which way is which, you can use the `axises` object.

You can declare one using a `figure` with the `axises` class. A plane has four optional parameters like `--width` and `--height` for its two dimentions, and `--length` and `--length2` for the dimensions of the axis themselves.

Code to add axises:
```html
<figure class="axises">
    <div class="axis axis-x">x</div>
    <div class="axis axis-y">y</div>
    <div class="axis axis-z">z</div>
</figure>
```

3. Plane

The biggest problem of the basic mesh is that the texture is reproduced on both sides. A plane allows for one texture on each side by superposing two basic meshes.

You can declare a plane by using a `figure` with the `plane` class. A plane has two parameters `--width` and `--height` for its two dimentions.

Example: A dual textured plane.
```html
<figure class="plane" style='--width: 100px; --height: 200px;'>
    <img class="face front" src="side1.png" />
    <img class="face back " src="side2.png" />
</figure>
```

4. Cube

Cubes are, well, cubes. It uses six square basic meshes to create one cube.

You can declare a plane by using a `figure` with the `cube` class. A plane has one parameter: `--size` for its verticle size.

Example: A cube with a texture on the front.
```html
<figure class="cube" style='--size: 200px;'>
    <img class="face front " src="side1.png" />
    <div class="face back  "></div>
    <div class="face right "></div>
    <div class="face left  "></div>
    <div class="face top   "></div>
    <div class="face bottom"></div>
</figure>
```

5. Cuboid Rectangular

They're like cubes, but with different dimensions for every side.

You can declare one by using a `figure` with the `cuboid rectangular` classes. It has has three parameter: 
- `--width` for its horizontal (x) size.
- `--length` for its vertical (y) size.
- `--depth` for its (z) size.

Example: A simple white cuboid rectangular with outlined verticles.
```html
<figure class="cuboid rectangular" style='--length: 7px; --width: 10px; --depth: 20px;'>
    <div class="face front " style="outline: solid 1px black;"></div>
    <div class="face back  " style="outline: solid 1px black;"></div>
    <div class="face left  " style="outline: solid 1px black;"></div>
    <div class="face right " style="outline: solid 1px black;"></div>
    <div class="face top   " style="outline: solid 1px black;"></div>
    <div class="face bottom" style="outline: solid 1px black;"></div>
</figure>
```

6. Cylinder

Cylinders in this framework work by using several simple meshes to make it an n-sides prism.

You can declare one by using a `figure` with the `cylinder` classes. It has has three parameter: 
- `--radius` for the radius of the base.
- `--height` for its vertical (y) size.
- `--strip-count` Number of stripes to use (24 by default, 90 max).

You can have the cylinder textured by adding the `textured` class, and linking an image in the `--texture` variable. Enecss will fill the stripes with the texture from left to right.

Example: A textured cylinder.
```html
<figure class="cylinder textured" style='--height: 170px; --radius: 18px; --strip-count: 24; --texture: url(/texture.png);'>
    <div class="strip strip-1"></div>
    <div class="strip strip-2"></div>
    <div class="strip strip-3"></div>
    <div class="strip strip-4"></div>
    <div class="strip strip-5"></div>
    <div class="strip strip-6"></div>
    <div class="strip strip-7"></div>
    <div class="strip strip-8"></div>
    <div class="strip strip-9"></div>
    <div class="strip strip-10"></div>
    <div class="strip strip-11"></div>
    <div class="strip strip-12"></div>
    <div class="strip strip-13"></div>
    <div class="strip strip-14"></div>
    <div class="strip strip-15"></div>
    <div class="strip strip-16"></div>
    <div class="strip strip-17"></div>
    <div class="strip strip-18"></div>
    <div class="strip strip-19"></div>
    <div class="strip strip-20"></div>
    <div class="strip strip-21"></div>
    <div class="strip strip-22"></div>
    <div class="strip strip-23"></div>
    <div class="strip strip-24"></div>
</figure>
```

**Note regarding editing objects**: I recommend using your web browser's dev tools to edit elements, then save the copy back the modified HTML from there.

### Parenting objects

When you use several objects, you can 'parent' them to one another (just like you would in any 3D editor), in the same way you would parent any node in HTML.

```html
<figure id="parent" style='transform: rotateY(30deg);'>
    <figure id="child" class="cube position-at-center" style='--size: 100px;'>
        <div class="face front " style="background: white;"></div>
        <div class="face back  " style="background: white;"></div>
        <div class="face right " style="background: white;"></div>
        <div class="face left  " style="background: white;"></div>
        <div class="face top   " style="background: white;"></div>
        <div class="face bottom" style="background: white;"></div>
    </figure>
</figure>
```

All the transformations of the parent will be applied to the child, which means in this case, the cube will be rotated 30° on the Y axis.

**Note**: The `position-at-center` class allow for objects that do NOT have applied transform to position themselves at the center of their parents. The same result can be achieved by prepending `translateX(-50%) translateY(-50%)` to the object's transform.

### Manipulating mesh

Every lowest level node is a 3D 'mesh' (a rectangular plane object, in this case). It is important to note that you can use *any* html element as a mesh.
- `div` will not provide anything by default
- `a` will make a 3D clickable link or state switcher (more on that later)
- `button` will allow for a clickable surface with a temporary state (more on that later)
- `img` will make for a texturable surface.
- `video` can make a 3D video player (no performance waranty though)

And best of all! They can be nested!

For example...
```html
<div class="face front">
    <img class="fill" src="texture.png"/>
    <a class="fill" href="#state1"></a>
</div>
```
... is a clickable textured element.

If you want to hide even a single mesh, you can use the `hidden` class, or even better.    
If you're not sure where a specific mesh is, you can add the `debug` class to it, which will add a red outline to the mesh.

### Basic interactivity

If you want to be able to rotate the object around using your mouse, you can add view sections nodes *on the same level as the scene node, just before it*.
```html
<div class="view-section view-top-0 view-left-0"></div>
<div class="view-section view-top-0 view-left-1"></div>
<div class="view-section view-top-0 view-left-2"></div>
<div class="view-section view-top-0 view-left-3"></div>
<div class="view-section view-top-0 view-left-4"></div>
<div class="view-section view-top-0 view-left-5"></div>
<div class="view-section view-top-0 view-left-6"></div>
<div class="view-section view-top-0 view-left-7"></div>
<div class="view-section view-top-0 view-left-8"></div>
<div class="view-section view-top-1 view-left-0"></div>
<div class="view-section view-top-1 view-left-1"></div>
<div class="view-section view-top-1 view-left-2"></div>
<div class="view-section view-top-1 view-left-3"></div>
...
<div class="view-section view-top-8 view-left-8"></div>
```

This divides the screen in 81 sections to allow for gradual rotation from the center of the scene.

### Advanced interactivity: States

'States' is the most advanced feature you can use to save interaction data in CSS. It's possible to use the location hashmap to save a current state which, best of all, can stay registered even if the user erases his cookies.

Though only one state can be detected at the time, it's possible to create multiple CSS variables that vary depending on the state.

#### Registering a new state

First of all, to register a state, you should create a new element *on the same level as the scene node, just before it*.

For instance:
```html
<div id="state1"></div>
...
<section class="scene">
```

And there you go! You have registered a new state. The `div`'s id is what will be refered as the state's name from now on.

#### Entering the state

In order to enter a state, there are two ways.

You can use Javascript (which kind of destroys the purpose) OR use an `a` element.
```html
<a href="#state1">Click me!</a>
```

By clicking the element, the user will be able to change the state of the scene.

As mentioned before, you can use `a` elements in meshes, meaning you can have *interactive meshes* that change the state of the scene.

For instance, on a plane:
```html
<figure class="plane">
    <div class="face front">
        <img class="fill" src="texture.png"/>
        <a class="fill" href="#state1"></a>
    </div>
    <div class="face back"></div>
</figure>
```

#### Detecting and Using States

Now that we know how to declare and enter states, let's get into the heart of the matter.
Detecting states is pretty easy: in your CSS file, we can use a combinasion of the `:target` element and the [General sibling combinator](https://developer.mozilla.org/en-US/docs/Web/CSS/General_sibling_combinator) to apply custom styles to the scene using states.

For instance:
```css
#state1:target ~ section.scene {
    /* custom styles here */
}
```

You can even apply styles to specific elements:
```css
#state1:target ~ section.scene #element {
    /* custom styles here */
}
```

#### Locking rotation

If you use many different kinds of of rotation, it might be a good idea to lock it based on certain states.

To do so, use the scene selector, and set the `--rotation-x` and `--rotation-y` to fixed `!important` values.

```css
#state1:target ~ section.scene {
    --rotation-x: -40deg !important;
    --rotation-y: 40deg !important;
}
```

If you're still having trouble with selecting interactive elements, you might add the class `interactive` to your root, or any large enough element to lock the location on the current default.

### Tooltips

Having tooltips can help the user know what they are pointing at. Any `interactive` element (with the class, or `a` or `button`) can have one, using a div with the `tooltip` class. You can apply transforms to the tooltip for it to appear exactly where you want it to.

Example:
```html
<figure class="cuboid rectangular interactive">
    ...
    <div class="tooltip" style="transform: translateY(-30px) translateX(-20px) translateZ(50px) rotateX(-90deg);">Click me!</div>
</figure>
```

## Examples

There is a sample cube example which makes use of practically everything you saw before in the `examples/cube` folder.

## F.A.Q.

### Why?

The question you're looking for is: "Why not?" I created this for fun, but maybe someone, somewhere, will find some use of this. Pretty sure there exists plenty of environements on the web that allows CSS and not JS.

### Enterprise Support?

No. At least, not for now.

### Shadows? Shaders? Raytracing?

✨Unimplementable✨ (at least with just CSS)

## Credits

This framework contains organised research led by various other people. In no particular order:

- Cylinder by [allenski on StackOverflow](https://stackoverflow.com/a/66130780)
- States by [Robin Rendle](https://css-tricks.com/a-whole-website-in-a-single-html-file/)



