<template>
  <div class="control-stick" :style="styleProps">
    <svg class="stick-area" :width="size" :height="size">
      <circle :cx="size/2" :cy="size/2" :r="(size - strokeWidth) / 2" :stroke-width="strokeWidth" stroke="black" stroke-opacity="0.1" fill="none"/>
      <polygon :points="octagonPoints" fill="black" fill-opacity="0.1" stroke="gray" :stroke-width="strokeWidth" />
    </svg>
    <svg class="stick-thumb" :style="stickThunbStyleProps" :width="size * thumbScalar" :height="size * thumbScalar">
      <circle :cx="size / 2 * thumbScalar" :cy="size / 2 * thumbScalar" :r="(size * thumbScalar - strokeWidth) / 2" :stroke-width="strokeWidth" stroke="green" stroke-opacity="0.5" fill="green"/>
    </svg>
  </div>
</template>

<script>
let x = 0, y = 0;

export default {
  props: ["size"],
  data() {
    return {
      strokeWidth: 5,
      thumbScalar: 0.3
    }
  },
  computed: {
    octagonPoints() {
      let center = this.size / 2;
      let radius = this.size / 2 - this.strokeWidth;
      let retString = "";

      for (let i = 0; i < 8; i++) {
        let cos = Math.cos(i / 4 * Math.PI);
        let sin = Math.sin(i / 4 * Math.PI);
        
        let px = center + cos * radius;
        let py = center + sin * radius;

        retString += `${px} ${py}, `;
      }
      return retString.slice(0, -2);
    },
    stickThunbStyleProps() {
      return {
        'left': `${(x+1) * this.size/2}px`,
        'top': `${(y+1) * this.size/2}px`,
        'margin-left': `${-this.size / 2 * this.thumbScalar}px`,
        'margin-top': `${-this.size / 2 * this.thumbScalar}px`
      }
    },
    styleProps() {
      return {
        'width': `${this.size}px`,
        'height': `${this.size}px`
      }
    }
  }
}
</script>

<style scoped>
.control-stick {
  display: inline-grid;
  margin: 10px;
  position: relative;
}

.stick-area {
  position: absolute;
}

.stick-thumb {
  position: absolute;
}
</style>
