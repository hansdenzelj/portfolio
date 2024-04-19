<script>
export default {
  props: {
    theme: {
      type: Object,
      default: () => ({
        foreground: "#000000",
        background: "#FFFFFF",
      }),
    },
    active: {
      type: Boolean,
      default: false,
    },
    project_id: Number,
  },
  data() {
    return {
      textcolor: "#000000",
      bgcolor: "#ffffff",
      image_index: 0,
    };
  },
  emits: ["close"],
  methods: {
    closeView() {
      if (self.active === true) {
        self.active = false;
      }
    },
    moveIndex(project_id, direction) {
      direction === 'right' ? this.image_index++ : this.image_index--;
      const length = this.getProject(project_id).img.length - 1;
      if (this.image_index < 0) 
        this.image_index = length;
      if (this.image_index > length)
        this.image_index = 0;
    },
    getImageUrl(imgFile) {
      return new URL(`../assets/${imgFile}`, import.meta.url).href
    },
    getProject(id) { 
      switch (id) {
        case 0:
          return {
            title: "Desert Ordering Site",
            tooling: "Made with HTML, Javascript and JQuery",
            description:
              "A simple desert ordering website with a shopping cart and an order placing function which sends a receipt through email.",
            img: ["project_1_0.png", "project_1_1.png"]
          };
        case 1:
          return {
            title: "Car Rental Site",
            tooling: "Made with PHP, HTML, Javascript",
            description: "A website concept for renting cars between users, definitely a bit too large of an undertaking as a solo project while juggling with other subjects.",
            img: ["project_2_0.png", "project_2_1.png", "project_2_2.png", "project_2_3.png", "project_2_4.png", "project_2_5.png"]
          };
        case 2:
          return {
            title: "Promotional Site",
            tooling: "Made with PHP, HTML, Javascript",
            description: "A small website project to promote a motorcycle.",
            img: ["project_5_0.png", "project_5_1.png", "project_5_2.png", "project_5_3.png"]
          };
        case 3:
          return {
            title: "Task Manager",
            tooling: "Made with React and Firebase",
            description:
              "A small group project CRUD app for managing tasks with authentication.",
            img: ["project_3_0.png", "project_3_1.png", "project_3_2.png"],
          };
        case 4:
          return {
            title: "Computer Vision Yoga App",
            tooling: "Made with Python, OpenCV, MediaPipe, Tensorflow and Kivy",
            description:
              "Our thesis project which uses machine learning and computer vision to make yoga more interactive.",
            img: ["project_4_0.png", "project_4_1.png", "project_4_2.png", "project_4_3.gif"],
          };
      }
    },
  },
  watch: {
    theme(color) {
      this.textcolor = color.foreground;
      this.bgcolor = color.background;
    },
    active() {
      this.image_index = 0;
    },
  },
};
</script>

<template>
  <div v-if="active" class="Project-Wrapper" @click.self="$emit('close')">
    <div class="Project" :style="{ 'background-color': bgcolor, color: textcolor }">
      <h1>{{ getProject(project_id)["title"] }}</h1>
      <p class="Project-Tooling" :style="{ color: textcolor }">
        {{ getProject(project_id)["tooling"] }}
      </p>
      <p class="Project-Description" :style="{ color: textcolor }">
        {{ getProject(project_id)["description"] }}
      </p>
      <div class="Project-Carousel">
        <Transition>
          <img :src="getImageUrl(getProject(project_id)['img'][image_index])" /> 
        </Transition>
        <div class="Carousel-Control">
          <button type="button" @click="moveIndex(project_id, 'left')">
            ←
          </button>
          <button type="button" @click="moveIndex(project_id, 'right')">
            →
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.Project-Wrapper {
  background-color: rgba(0, 0, 0, 0.85);
  position: fixed;
  z-index: 998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.Project {
  z-index: 999;
  width: 800px;
  height: auto;
  background-color: white;
  border-radius: 8px;
  padding: 1em;
}

.Project-Tooling {
  font-size: clamp(0.6rem, 1.5vw, 0.8rem);
  margin-bottom: 0.4em;
}

.Project-Carousel {
  display: flex;
  flex-direction: column;
  margin: 1.8em auto;  
  align-items: center;
  justify-content: center;
}

.Carousel-Control {
  display: flex;
  width: 60%;
  margin: 0 auto;
  justify-content: flex-end;
  flex-direction: row;
  background-color: rgba(0, 0, 0, 0.2);
}

.Carousel-Control button {
  height: 100%;
  background-color: rgba(0, 0, 0, 0.2);
  border: none;
  transition: background-color 100ms ease;
  font-family: shippori-antique;
  font-size: clamp(0.6rem, 2vw, 1rem);
}

.Carousel-Control button:hover {
  background-color: rgba(255, 255, 255, 0.2);
}

img {
  width: 60%;
  max-width: 480px;
  min-height: 300px;
  transition: src 0.5s ease;
}

h1 {
  text-align: left;
  font-style: oblique;
  margin: 0em 0 0 0;
  font-size: clamp(1.8rem, 4vw, 2.2rem);
}

p {
  color: #000;
  margin: 0;
  white-space: pre-line;
  text-align: justify;
  font-size: clamp(0.8rem, 2vw, 1rem);
}

@media (max-width: 1000px) {
  .Project {
    width: 80%;
  }
}

@media (max-width: 900px) {
  img {
    min-height: auto;
  }
}
</style>
