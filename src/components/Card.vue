<script>
export default {
  components: {},
  props: {
    theme: {
      type: Object,
      default: () => ({
        foreground: "#000000",
        background: "#FFFFFF",
      }),
    },
    image_src: String,
    image_pos: String,
    project_id: Number,
  },
  data() {
    return {
      active: false,
    };
  },
  emits: ["setTheme", "unsetTheme", "clickEvent"],
  methods: {
    emitSetBGColor() {
      this.$emit("setTheme", [this.theme.background, this.theme.foreground]);
    },
    emitUnsetBGColor() {
      this.$emit("unsetTheme");
    },
    openArticle(articleRef) {
      console.log(this.image_src);
    },
  },
  watch: {
    active(state) {
      state ? this.emitSetBGColor() : this.emitUnsetBGColor();
    },
  },
};
</script>

<template>
  <div class="Card-Wrapper">
    <div
      class="Card"
      @click="this.$emit('clickEvent')"
      @mouseenter="active = true"
      @mouseleave="active = false"
      :style="{
        'background-image': `url(${this.image_src})`,
        'background-position': this.image_pos,
        'background-color': this.theme.background,
        color: this.theme.foreground,
      }"
    ></div>
    <div class="Card-Info">
      <slot class="Card-Title" name="title">
        <p>Insert Content Here</p>
      </slot>
    </div>
  </div>
</template>

<style scoped>
p {
  margin: 0;
}

.Card {
  min-width: 100px;
  width: 100%;
  min-height: 500px;
  height: auto;
  padding: 0.5em;
  border-radius: 10px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  transition: transform 200ms;
  display: flex;

  flex-direction: column;
  font-size: clamp(1rem, 2.5vw, 2rem);

  background-position: bottom;
  background-size: contain;
  background-repeat: no-repeat;
}

.Card-Info {
  margin-top: 10px;

  font-size: clamp(1rem, 1.2rem, 3rem);

  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.Card-Title {
  font-size: clamp(1rem, 1.8rem, 3rem);

  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.Card:hover {
  /* border: 0.2em solid rgb(223, 223, 223) */
  transform: scaleX(102%) scaleY(102%);
}

img {
  align-self: flex-start;
}

@media (max-width: 767px) {
  .Card {
    min-height: 300px;
  }
}

@media (min-width: 768px) {
  .Card {
    min-height: 300px;
  }
}

@media (min-width: 1024px) {
  .Card {
    min-height: 350px;
  }
}

@media (min-width: 1280px) {
  .Card {
    min-height: 375px;
  }
}

@media (min-width: 1536px) {
  .Card {
    min-height: 400px;
  }
}

@media (min-width: 1920px) {
  .Card {
    min-height: 500px;
  }
}

@media (min-width: 2560px) {
  .Project {
    width: 50%;
  }
}

@media (min-width: 3440px) {
  .Project {
    width: 40%;
  }
}
</style>
