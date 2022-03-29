# slidev-presentations
some notes on using slidev

Main link to [slidev](https://sli.dev/)

## Some links

 - [TailwindCSS helper](https://tailwindcomponents.com/cheatsheet/) very close to Windy CSS.
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

###  Plotly interactive 3D surface

First install it with `npm install plty.js-dist`

create a file called `plotsimple.vue` in the `components` folder with the following content:

```js
<template>
  <div>
    <div ref="plot1" id="plot1"></div>
  </div>
</template>

<script>
import  Plotly  from 'plotly.js-dist';

var data = [{
           z: [[0.542974751519751,0.2856731165654307,0.21596014487368428,0.19543836116878094,0.17247053411206434,0.16135062082262483,0.13219484569182371,0.08618705675864953,0.06864835725033576,0.08298077224326074],[0.1435799544604807,0.2341096376246262,0.28217466923969436,0.23402597964815802,0.22444128467289934,0.24208314618250623,0.13632585002015538,0.08476504635173922,0.048349217797679755,0.011602441106242353],[0.19993639506230804,0.24012219112980276,0.19403712236749154,0.23740484616358193,0.22145034051497137,0.1099816098222654,0.19333157682138433,0.11965123560699722,0.08017762936345393,0.0430757669580774],[0.060128421674379984,0.14105042687847413,0.15173385265854614,0.17194110329476725,0.15500086876373237,0.1162971599952693,0.19961626960953682,0.22422898948520725,0.2054534547802487,0.10159541409775376],[0.027531360464606868,0.06420946629151499,0.09464261959958295,0.09707537912286471,0.11968852551553265,0.2091220283733534,0.16770682065911735,0.23314918694266004,0.29940878552139993,0.28219467625540945],[0.025849116818473426,0.0348351615101512,0.06145159126100073,0.06411433060184706,0.10694844642079987,0.16116543480398085,0.17082463719798247,0.25201848485474676,0.29796255528688204,0.47855092933925625]],
           x: [1,2,3,4,5,6,7,8,9,10],
           y: [1,2,3,4,5,6],       
           type: 'surface',
           showscale: false,
           showlegend: false,
        }];

var layout = {
  title: '',
  scene: {
    xaxis:{
      title: 'firms',
      tickvals:[1,2,3,4,5,6,7,8,9,10]
    },
    yaxis:{title: 'workers'},
    zaxis:{title: ''},
    aspectratio:{x:1, y:1, z:0.6},
    camera: {
      center: {
            x: 0, y: 0, z: -0.36}, 
      eye: { 
            x:-1.5, y:-1.5, z:1.5}, 
    },
  },
  autosize: false,
  width: 900,
  height: 600,
  margin: {
    l: 0,
    r: 0,
    b: 50,
    t: 0,
  },
  modebar: {
    // vertical modebar button layout
    orientation: 'v',
    activecolor: '#9ED3CD'
  },
}

export default {
  name: "PlotlyTestv2",
  data: function() {
    return {
      count: 0,
      data:[{ x: [1,2,3,4], y: [10,15,13,17], type:"scatter" }],
      attr: { displayModeBar: true },
      layout: { title: "My graph :)" }
    };
  },
  mounted() {
    Plotly.newPlot(this.$refs.plot1, data, layout);
  }
}
</script>

```

you can then simply use the `<plotsimple />` tag in inside your `slides.md` file.

