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
