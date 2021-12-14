<template>
  <div class="grid">
    <Image v-for="n in 9" :key="`image-${n}`" :index="n" />
  </div>
</template>

<script>
import Image from "./Image.vue";

export default {
  name: "HelloWorld",
  components: {
    Image,
  },
};
</script>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: auto auto auto auto;
}
</style>
