<template>
  <div>
    <button
      v-on:click="goto"
      class="
        text-white
        rounded
        bg-blue-500
        px-2
        py-1
        shadow-lg
        focus:outline-none
      "
    >
      {{ text }}
    </button>
  </div>
</template>
 
<script>
import routes from "/@slidev/routes";
// import { router } from '/@slidev/client'

export default {
  props: ["target", "text"],
  data() {
    return {
      routes: routes,
      targetSlideNumber: -1,
    };
  },
  mounted() {
    const dest = this.routes.find(
      (element) => element.meta?.label == this.target
    );
    this.targetSlideNumber = parseInt(dest.path);
  },
  methods: {
    goto: function (event) {
      // find the slide
      const dest = this.routes.find(
        (element) => element.meta?.label == this.target
      );

      if (dest === undefined) {
        alert("could not find target:" + this.target);
      }
      this.$slidev.nav.go(parseInt(dest.path));
    },
  },
};
</script>
