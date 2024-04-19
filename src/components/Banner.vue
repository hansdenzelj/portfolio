<script>
export default {
  props: {
    accentColor: {
      type: String,
      default: "#FFFFFF",
    },
  },
};
</script>

<template>
  <div class="navbar">
    <div class="info">
      <div class="heading">
        <div class="logo">
          <div>H</div>
          <div>A</div>
          <div>N</div>
          <div>S</div>
        </div>
        <div class="name">
          <h1>Hans Denzel Jimenez</h1>
          <h3>Aspiring Software Developer</h3>
        </div>
      </div>
      <div class="description">
        <h2>About Me</h2>
        <!-- <hr :style="{ 'background-color': this.accentColor }" /> -->
        <p style="text-align: justify">
          I live in Quezon City,
          I am a student currently taking up a Bachelor's Degree in Computer Science at
          CIIT College of Arts and Technology.
        </p>
      </div>
      <div class="description">
        <h2>Vision</h2>
        <!-- <hr :style="{ 'background-color': this.accentColor }" /> -->
        <p style="text-align: justify">
          I want to become a software developer that is capable of building
          practical applications with real world use. Through the medium of
          software, I aim to make solutions to better people's lives through
          efficiency, the streamlining of processes and the likes. In addition,
          I would also like to provide entertainment and recreational value by
          creating software.
        </p>
      </div>
    </div>
    <div :class="`accent`" >
    </div>
  </div>
  
</template>

<style scoped>
h1 {
  margin: 0;
}

h2 {
  margin: 0 0 0.2em 0;
}

h3 {
  margin: 0;
}

.header-content {
  display: flex;
}

.heading {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 1em;
}

.logo {
  max-width: 100px;
  display: grid;
  grid-template-columns: auto auto;
  text-align: left;
  font-size: 40px;
}

.logo div {
  line-height: 0.8;
  user-select: none;
}

.name {
  text-align: right;
  width: 100%;
}

.description>h2 {
  text-align: left;
}

p {
  margin: 0;
}

hr {
  border: none;
  height: 1px;
}

.info {
  display: grid;
  /* grid-template-columns: 0.5fr 1fr 1fr; */
  grid-template-rows: repeat(1fr, 3);
  gap: 1rem;
  margin: 0 1em;
  margin-right: 2em;
}

.accent {
  width: 100%;
  height: 100%;
  background: url('../assets/pattern.png') repeat;
}

.accent::after {
  content: ""; /* Allows psuedo element to show */
  background: #EC008C; /* The color you want the icon to change to */
  mix-blend-mode: multiply;
}

.navbar {
  position: sticky;
  padding: 1em;
  background-color: rgba(0, 0, 0, 0.1);
  display: grid;
  grid-template-columns: 40% 60%;
}


.navbar-scrolled {
  background-color: rgba(0, 0, 0, 0.5);
}

@media ((max-width: 1800px)) {
  .info {
    grid-template-columns: none;
    grid-template-rows: 1fr, 1fr, 1fr;
    gap: 2rem;
  }

  .navbar {
    grid-template-columns: 50% 50%;
  }
} 

@media ((max-width: 1500px)) {
  .navbar {
    grid-template-columns: 60% 40%;
  }
}

@media ((max-width: 1200px)) {
  .navbar {
    grid-template-columns: 70% 30%;
  }
}

@media ((max-width: 900px)) {
  .navbar {
    grid-template-columns: 100% 0%;
  }
}

@media ((max-width: 650px)) {
  .heading {
    flex-direction: column;
  }
  
  .logo {
    margin: 0 auto;
  }

  .name {
    text-align: center
  }
}
</style>
