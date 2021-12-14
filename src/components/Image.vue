<template>
  <div class="card">
    <img
      :id="`target-image-${index}`"
      :src="`https://picsum.photos/250/200?image=${index * 5 + 10}`"
      @load="getPalette()"
    />
    <div class="text" v-show="!loading">
      <div class="title-line">
        <h2 :style="{ color: dark }">Title</h2>
        <Star class="star" :fill="accent" />
      </div>
      <p :style="{ color: light }">This is a nice little description of the image</p>
    </div>
  </div>
</template>

<script>
import Vibrant from "node-vibrant";
import Star from "./Star.vue";

export default {
  name: "HelloWorld",
  props: {
    index: Number,
  },
  components: {
    Star,
  },
  data: () => {
    return {
      palette: {}
    };
  },
  methods: {
    getPalette() {
      const img = document.getElementById(`target-image-${this.index}`);
      const vibrant = new Vibrant(img);

      img.setAttribute('crossOrigin', 'anonymous')

      vibrant.getPalette().then(
        (palette) => this.palette = palette,
        (reason) => {
          console.error(reason);
        }
      )
    },
  },
  computed: {
    dark() {
      if (!this.palette || !this.palette.DarkVibrant) {
        return `black`;
      }
      return this.palette.DarkVibrant.getHex();
    },
    light() {
      if (!this.palette || !this.palette.LightMuted) {
        return `lightgrey`;
      }
      return this.palette.LightMuted.getHex();
    },
    accent() {
      if (!this.palette || !this.palette.Vibrant) {
        return `crimson`;
      }
      return this.palette.Vibrant.getHex();
    },
  },
};
</script>

<style scoped>
* {
  transition: 0.3 color ease;
}

h2 {
  font-weight: 300;
}

.card {
  border-radius: 8px;
  box-shadow: 5px 10px 10px rgb(231, 227, 227);
  display: flex;
  flex-direction: column;

  margin-bottom: 32px;
  width: 250px;
}

img {
  border-radius: 8px 8px 0 0;
}

.text {
  margin: 0 16px;
}

.title-line {
  display: flex;
  justify-content: space-between;
}

.star {
  margin-top: 24px;
}
</style>
