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
  props: ["size", "player", "keyUp", "keyDown", "keyLeft", "keyRight"],
  mounted() {
    document.addEventListener("mouseup", this.thumbMouseUp);
    document.addEventListener("mousemove", this.thumbMove);
    this.stickThumb = this.$el.querySelector(".stick-thumb");
    this.updateThumb();
  },
  data() {
    return {
      strokeWidth: 5,
      thumbScalar: 0.7,
      thumbX: 0,
      thumbY: 0,
      isClicked: false,
      stickThumb: undefined,
      downKeys: { up: false, down: false, left: false, right: false },
      deadzone: 0.4
    };
  },
  computed: {
    octagonPoints() {
      const center = this.size / 2;
      const radius = this.size / 2 - this.strokeWidth;
      let retString = "";

      for (let i = 0; i < 8; i++) {
        const cos = Math.cos((i / 4) * Math.PI);
        const sin = Math.sin((i / 4) * Math.PI);

        const px = center + cos * radius;
        const py = center + sin * radius;

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

      const scalar = 2 / this.size / (1 - this.thumbScalar);
      
      this.thumbX += e.movementX * scalar;
      this.thumbY += e.movementY * scalar;
    },
    updateThumb() {
      this.setThumbPos();
      this.updateKeys();
    },
    setThumbPos() {
      let realX = this.thumbX,
        realY = this.thumbY;

      const dist = Math.sqrt(realX * realX + realY * realY);
      if (dist > 1) {
        realX /= dist;
        realY /= dist;
      }

      const posX = ((realX * (1 - this.thumbScalar) + 1) * this.size) / 2;
      const posY = ((realY * (1 - this.thumbScalar) + 1) * this.size) / 2;
      this.stickThumb.style.left = `${posX}px`;
      this.stickThumb.style.top = `${posY}px`;
    },
    updateKeys() {
      let newDownKeys = {};

      const distSquared = this.thumbX * this.thumbX + this.thumbY * this.thumbY;
      if (distSquared > this.deadzone * this.deadzone) {
        const angle = Math.atan2(this.thumbY, this.thumbX);
        newDownKeys.up = angle <= -Math.PI / 6 && angle >= (-5 * Math.PI) / 6;
        newDownKeys.down = angle >= Math.PI / 6 && angle <= (5 * Math.PI) / 6;
        newDownKeys.right = angle >= -Math.PI / 3 && angle <= Math.PI / 3;
        newDownKeys.left =
          angle >= (2 * Math.PI) / 3 || angle <= (-2 * Math.PI) / 3;
      } else {
        newDownKeys.up = false;
        newDownKeys.down = false;
        newDownKeys.right = false;
        newDownKeys.left = false;
      }
      this.downKeys = newDownKeys;
    },
    CREvent(eventType, keyCode) {
      // ruffle needs to be clicked into focus to register keyboard events
      const pointerEvent = new PointerEvent("pointerdown");
      this.player.dispatchEvent(pointerEvent);

      var e = new Event(eventType);
      e.key = "";
      e.code = keyCode;
      window.dispatchEvent(e);
    }
  },
  watch: {
    thumbX() {
      this.updateThumb();
    },
    thumbY() {
      this.updateThumb();
    },
    downKeys: {
      handler(newKeys, oldKeys) {
        if (newKeys.up != oldKeys.up) {
          this.CREvent(newKeys.up ? "keydown" : "keyup", this.keyUp);
        }
        if (newKeys.down != oldKeys.down) {
          this.CREvent(newKeys.down ? "keydown" : "keyup", this.keyDown);
        }
        if (newKeys.left != oldKeys.left) {
          this.CREvent(newKeys.left ? "keydown" : "keyup", this.keyLeft);
        }
        if (newKeys.right != oldKeys.right) {
          this.CREvent(newKeys.right ? "keydown" : "keyup", this.keyRight);
        }
      },
      deep: true
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
