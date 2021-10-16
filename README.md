# slidev-presentations
some notes on using slidev

Main link to [slidev](https://sli.dev/)

## Some links

 - [WindiCSS helper](https://tailwindcomponents.com/cheatsheet/)
 - [icon search](https://icones.js.org/)

## Images / plots

### Using static files 

 - put in the image in the `public` folder
 - point to the image in `<img src="/myimage.png" />`
 - see [documentation](https://vitejs.dev/guide/assets.html#static-asset-handling)

### Styling

styling can be done using WindiCSS, just add terms to the class attribute

 - center the image with `<img src="/myplot.png" class="mx-auto"/>`
 - you can also control the size with class `w-50` or `h-50` and adjust the number
 - you can add shadow, rounder corners, border, padding, etc ... 

a complete example looks like:

```js
<img src="/myplot.png" class="m-3 p-3 mx-auto w-90 shadow-xl border-grey border rounded" />
```

### Using Dynamic path

This is if you don't know the filename at build time. You can use the following solution:

```js
const imgUrl = new URL('./img.png', import.meta.url).href
```

see [documentation](https://vitejs.dev/guide/assets.html#static-asset-handling)



## Custom components

### Link

The `Link.vue` component allows you to add a link to another slide by simply using `<Link target="slide_label" text="go there" />` where `slide_label` is added as a label property to the front matter of one of your slides. To use, copy the file to your `components` folder and then write something like:

```md

---
label: slide_a
---

# Hello, this is Slide A

some content

--- 

# Other slide

<Link target="slide_a" text="go to slide A" />

```
