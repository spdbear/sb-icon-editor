<template>
  <div id="app">
    <!-- <HelloWorld /> -->
    <h1>Bear Icon Generator</h1>
    <p>
      bgsize:
      <input type="number" min="8" max="1920" v-model="bgsize" />
      <input type="range" min="8" max="1920" v-model="bgsize" />
    </p>
    <svg viewBox="0 0 500 500" :width="bgsize" :height="bgsize" :style="bgstyle">
      <!-- <line :x1="x1" y1="100" x2="200" y2="200" stroke="black" /> -->
      <circle cx="250" cy="250" :r="r0" :fill="color" :stroke-width="stroke" />
      <circle cx="250" cy="250" :r="rad" :stroke="color" fill="none" :stroke-width="stroke" />
      <circle :cx="cx2" :cy="cy2" :r="r2" :stroke="color" fill="none" :stroke-width="stroke" />
      <circle :cx="cx3" :cy="cy2" :r="r3" :stroke="color" fill="none" :stroke-width="stroke" />
    </svg>

    <p>
      radius:
      <input type="number" min="10" max="200" v-model="rad" />
      <input type="range" min="10" max="200" v-model="rad" />
    </p>
    <p>
      stroke:
      <input type="number" min="10" max="100" v-model="stroke" />
      <input type="range" min="10" max="100" v-model="stroke" />
    </p>
    <p>
      theta:
      <input type="number" min="0" max="360" v-model="theta" />
      <input type="range" min="0" max="360" v-model="theta" />
    </p>
    <p>
      color: {{color}}
      <input type="color" name="head" v-model="color" />
    </p>
    <p>
      bgcolor: {{bgcolor}}
      <input type="color" name="head" v-model="bgcolor" />
    </p>
  </div>
</template>

<script>
export default {
  name: "App",
  data: function() {
    return {
      bgsize: 500,
      rad: 100,
      stroke: 20,
      theta: 45,
      color: "#008101",
      bgcolor: "#eeeeee"
    };
  },
  computed: {
    r0: function() {
      return this.rad / 1.618 / 1.618 / 1.618;
    },
    r2: function() {
      return this.rad / 1.618 / 1.618;
    },
    r3: function() {
      return this.rad / 1.618;
    },
    cx2: function() {
      return 250 - this.rad * Math.sin((this.theta * Math.PI) / 180);
    },
    cx3: function() {
      return 250 + this.rad * Math.sin((this.theta * Math.PI) / 180);
    },
    cy2: function() {
      return 250 - this.rad * Math.cos((this.theta * Math.PI) / 180);
    },
    bgstyle: function() {
      return "background: " + this.bgcolor;
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
