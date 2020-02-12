<template>
  <div id="app">
    <!-- <HelloWorld /> -->
    <h1>Bear Icon Generator</h1>
    <svg
      id="bearsvg"
      viewBox="0 0 500 500"
      :width="bgsize"
      :height="bgsize"
      :style="bgstyle"
    >
      <!-- <line :x1="x1" y1="100" x2="200" y2="200" stroke="black" /> -->
      <circle cx="250" :cy="cy" :r="r0" :fill="color" :stroke-width="stroke" />
      <circle
        cx="250"
        :cy="cy"
        :r="rad"
        :stroke="color"
        fill="none"
        :stroke-width="stroke"
      />
      <circle
        :cx="cx2"
        :cy="cy2"
        :r="r2"
        :stroke="color"
        fill="none"
        :stroke-width="stroke"
      />
      <circle
        :cx="cx3"
        :cy="cy2"
        :r="r3"
        :stroke="color"
        fill="none"
        :stroke-width="stroke"
      />
      <circle
        cx="250"
        cy="250"
        :r="250"
        fill="none"
        stroke="#000"
        :stroke-width="previewCircleStroke"
      />
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
      y_cor:
      <input type="number" min="-250" max="250" v-model="y_cor" />
      <input type="range" min="-250" max="250" v-model="y_cor" />
    </p>
    <p>
      color: {{ color }}
      <input type="color" name="head" v-model="color" />
    </p>
    <p>
      bgcolor: {{ bgcolor }}
      <input type="color" name="head" v-model="bgcolor" />
    </p>
    <p>
      <button v-on:click="swapColor">Swap Color</button>
      Preview circle: <input type="checkbox" id="checkbox" v-model="checked" />
    </p>
    <p>
      Output Size:
      <input type="number" min="8" max="1920" v-model="bgsize" />
      <input type="range" min="8" max="1920" v-model="bgsize" />

      <button v-on:click="downloadSvg">Download as PNG</button>
    </p>
  </div>
</template>

<script>
import ssap from "save-svg-as-png";

export default {
  name: "App",
  data: function() {
    return {
      bgsize: 500,
      rad: 150,
      stroke: 36,
      theta: 45,
      y_cor: 20,
      color: "#35485e",
      bgcolor: "#41b883",
      checked: false
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
    cy: function() {
      return 250 + Number(this.y_cor);
    },
    cy2: function() {
      return this.cy - this.rad * Math.cos((this.theta * Math.PI) / 180);
    },
    bgstyle: function() {
      return `background: ${this.bgcolor}`;
    },
    previewCircleStroke: function() {
      const stroke = this.checked ? 1 : 0;
      return stroke;
    }
  },
  methods: {
    downloadSvg: function() {
      const name = `${this.bgsize}x${this.bgsize}-r${this.rad}-s${this.stroke}-t${this.theta}-y${this.y_cor}-${this.color}-${this.bgcolor}`;
      ssap.saveSvgAsPng(document.getElementById("bearsvg"), `${name}.png`);
    },
    swapColor: function() {
      const tmpMainColor = this.color;
      this.color = this.bgcolor;
      this.bgcolor = tmpMainColor;
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
