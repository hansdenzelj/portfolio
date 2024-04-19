<script>
import Float from "./components/Float.vue";
import Banner from "./components/Banner.vue";
import CardContainer from "./components/CardContainer.vue";
import Card from "./components/Card.vue";
import Foot from "./components/Foot.vue";
import ProjectView from "./components/ProjectView.vue";

export default {
	components: {
		Float,
		Banner,
		CardContainer,
		Card,
		ProjectView,
		Foot,
	},
	data() {
		return {
			default_textcolor: "#FFFFFF",
			default_bgcolor: "#242424",
			bgcolor: "#242424",
			textcolor: "#FFFFFF",
			lastbgcolor: "",
			lasttextcolor: "",
			project_active: false,
			project_id: 0,
		};
	},
	methods: {
		setTheme(color) {
			this.bgcolor = changeColor(color[0], -20);
			this.textcolor = color[1];
			this.lastbgcolor = changeColor(color[0], -20);
			this.lasttextcolor = color[1];
		},
		unsetTheme() {
			this.bgcolor = this.default_bgcolor;
			this.textcolor = this.default_textcolor;
		},
		showProject(id) {
			this.project_active = !this.project_active;
			this.project_id = id;
		},
	},
};

//Function to darken colors, courtesy of:
//https://stackoverflow.com/questions/62515517/darken-and-lighten-colors-in-javascript

function changeColor(color, amount) {
	// #FFF not supportet rather use #FFFFFF
	const clamp = (val) => Math.min(Math.max(val, 0), 0xff);
	const fill = (str) => ("00" + str).slice(-2);

	const num = Number.parseInt(color.substr(1), 16);
	const red = clamp((num >> 16) + amount);
	const green = clamp(((num >> 8) & 0x00ff) + amount);
	const blue = clamp((num & 0x0000ff) + amount);
	return (
		"#" +
		fill(red.toString(16)) +
		fill(green.toString(16)) +
		fill(blue.toString(16))
	);
}
</script>

<template>
  <div
    class="app-wrapper"
    :style="{ 'background-color': this.bgcolor, color: this.textcolor }"
  >
    <ProjectView
      :active="this.project_active"
      @close="this.project_active = false"
      :theme="{background: this.lastbgcolor, foreground: this.lasttextcolor}"
      :project_id=this.project_id
    />

    <header>
      <Banner :accentColor="this.textcolor" />
    </header>

    <main>
      <section class="section-project">
        <h1 class="section-label">Some Projects</h1>
        <CardContainer>
          <Card
            @setTheme="(color) => setTheme(color)"
            @unsetTheme="unsetTheme()"
            @clickEvent="showProject(0)"
            :theme="{
              foreground: 'black',
              background: '#ffe4e1',
            }"
            image_src="project_1.png"
            image_pos="center"
            :project_id=0
          >
            <template #title>Desert Ordering Site</template>
          </Card>

          <Card
            @setTheme="(color) => setTheme(color)"
            @unsetTheme="unsetTheme()"
            @clickEvent="showProject(1)"
            :theme="{
              foreground: 'white',
              background: '#ec2c01',
            }"
            image_src="project_2.png"
            image_pos="center"
            :project_id=1
          >
            <template #title>Car Rental Site</template>
          </Card>

          <Card
            @setTheme="(color) => setTheme(color)"
            @unsetTheme="unsetTheme()"
            @clickEvent="showProject(2)"
            :theme="{
              foreground: 'black',
              background: '#b9babe',
            }"
            image_src="project_5.png"
            image_pos="center"
            :project_id=2
          >
            <template #title>Promotional Site</template>
          </Card>

          <Card
            @setTheme="(color) => setTheme(color)"
            @unsetTheme="unsetTheme()"
            @clickEvent="showProject(3)"
            :theme="{
              foreground: 'white',
              background: '#027898',
            }"
            image_src="project_3.png"
            image_pos="center"
            :project_id=3
          >
            <template #title>Task Manager</template>
          </Card>

          <Card
            @setTheme="(color) => setTheme(color)"
            @unsetTheme="unsetTheme()"
            @clickEvent="showProject(4)"
            :theme="{
              foreground: 'black',
              background: '#e6e4e0',
            }"
            image_src="project_4.png"
            image_pos="center"
            :project_id=4
          >
            <template #title>CV Yoga App</template>
          </Card>
        </CardContainer>
      </section>
    </main>

    <footer>
      <Foot />
    </footer>
  </div>
</template>

<style scoped>
body > footer {
  position: sticky;
  top: 100vh;
}

main {
  padding: 0 1em 1em 1em;
  margin: 0 0 4em 0;
}

span {
  font-size: clamp(1rem, 2.5vw, 2rem);
}

footer {
  margin-top: auto;
  align-self: flex-end;
  width: 100%;
}

.app-wrapper {
  display: flex;
  flex-direction: column;
  transition: background-color 250ms;
  /* max-width: 80%; */
  margin: 0 auto;
  min-height: 100vh;
}

.section-label {
  margin-left: 1rem;
}
</style>
