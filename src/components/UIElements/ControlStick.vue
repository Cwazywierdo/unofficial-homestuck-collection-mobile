<template>
  <div class="control-stick" :style="styleProps">
    <svg :width="size" :height="size">
      <circle
        :cx="size / 2"
        :cy="size / 2"
        :r="(size - strokeWidth) / 2"
        :stroke-width="strokeWidth"
        stroke="black"
        stroke-opacity="0.1"
        fill="none"
      />
      <polygon
        :points="octagonPoints"
        fill="black"
        fill-opacity="0.1"
        stroke="gray"
        :stroke-width="strokeWidth"
      />
      <circle
        :cx="size / 2"
        :cy="size / 2"
        :r="(size * thumbScalar - strokeWidth) / 2"
        fill="gray"
      />
    </svg>
    <svg
      class="stick-thumb"
      :style="stickThunbStyleProps"
      @mousedown="thumbMouseDown"
      :width="size * thumbScalar"
      :height="size * thumbScalar"
    >
      <circle
        :cx="(size / 2) * thumbScalar"
        :cy="(size / 2) * thumbScalar"
        :r="(size * thumbScalar - strokeWidth) / 2"
        :stroke-width="strokeWidth"
        stroke="green"
        stroke-opacity="1"
        fill="lightgreen"
      />
    </svg>
  </div>
</template>

<script>
export default {
  props: ["size"],
  mounted() {
    document.onmouseup = this.thumbMouseUp;
    document.onmousemove = this.thumbMove;
    this.stickThumb = this.$el.querySelector(".stick-thumb");
    this.setThumbPos();
  },
  data() {
    return {
      strokeWidth: 5,
      thumbScalar: 0.4,
      thumbX: 0,
      thumbY: 0,
      isClicked: false,
      stickThumb: undefined
    };
  },
  computed: {
    octagonPoints() {
      let center = this.size / 2;
      let radius = this.size / 2 - this.strokeWidth;
      let retString = "";

      for (let i = 0; i < 8; i++) {
        let cos = Math.cos((i / 4) * Math.PI);
        let sin = Math.sin((i / 4) * Math.PI);

        let px = center + cos * radius;
        let py = center + sin * radius;

        retString += `${px} ${py}, `;
      }
      return retString.slice(0, -2);
    },
    stickThunbStyleProps() {
      return {
        "margin-left": `${(-this.size / 2) * this.thumbScalar}px`,
        "margin-top": `${(-this.size / 2) * this.thumbScalar}px`
      };
    },
    styleProps() {
      return {
        width: `${this.size}px`,
        height: `${this.size}px`
      };
    }
  },
  methods: {
    thumbMouseDown() {
      this.isClicked = true;
    },
    thumbMouseUp() {
      this.isClicked = false;
      this.thumbX = 0;
      this.thumbY = 0;
    },
    thumbMove(e) {
      if (!this.isClicked) return;

      let scalar = 2 / this.size;
      this.thumbX += e.movementX * scalar;
      this.thumbY += e.movementY * scalar;
    },
    setThumbPos() {
      let realX = this.thumbX,
        realY = this.thumbY;

      let dist = realX * realX + realY * realY;
      if (dist > 1) {
        dist = Math.sqrt(dist);
        realX /= dist;
        realY /= dist;
      }

      this.stickThumb.style.left = `${((realX + 1) * this.size) / 2}px`;
      this.stickThumb.style.top = `${((realY + 1) * this.size) / 2}px`;
    }
  },
  watch: {
    thumbX() {
      this.setThumbPos();
    },
    thumbY() {
      this.setThumbPos();
    }
  }
};
</script>

<style scoped>
.control-stick {
  display: inline-grid;
  margin: 10px;
  position: relative;
  touch-action: none;
}

.control-stick > * {
  position: absolute;
}
</style>
