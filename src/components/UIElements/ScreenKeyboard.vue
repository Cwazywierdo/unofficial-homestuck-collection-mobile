<template>
  <div>
    <div id="keyboard-wrapper" :style="cssProps">
    </div>
    <button id="show-keyboard" @click="isShowingFull = !isShowingFull">{{ isShowingFull ? "Hide" : "Show" }} Full</button>
  </div>
</template>

<script>
import Vue from 'vue'
import KeyButton from '@/components/UIElements/KeyButton.vue'

const allKeys = ["Escape","F1","F2","F3","F4","F5","F6","F7","F8","F9","F10","F11","F12","Backquote","Digit1","Digit2","Digit3","Digit4","Digit5","Digit6","Digit7","Digit8","Digit9","Digit0","Minus","Equal","Backspace","Tab","KeyQ","KeyW","KeyE","KeyR","KeyT","KeyY","KeyU","KeyI","KeyO","KeyP","BracketLeft","BracketRight","Backslash","CapsLock","KeyA","KeyS","KeyD","KeyF","KeyG","KeyH","KeyJ","KeyK","KeyL","Semicolon","Quote","Enter","ShiftLeft","KeyZ","KeyX","KeyC","KeyV","KeyB","KeyN","KeyM","Comma","Period","Slash","ShiftRight","ControlLeft","AltLeft","AltRight","ControlRight","Space","Insert","Delete","ScrollLock","Home","End","Pause","PageUp","PageDown","ArrowLeft","ArrowUp","ArrowDown","ArrowRight","Numpad7","Numpad8","Numpad9","NumpadAdd","NumpadAdd","Numpad4","Numpad5","Numpad6","NumpadSubtract","Numpad1","Numpad2","Numpad3","NumpadMultiply","Numpad0","NumpadDecimal","NumpadDivide"]

export default {
  components: { KeyButton },
  props: ["player", "keys", "width"],
  updated() {
    this.setupKeyboard();
  },
  mounted() {
    this.setupKeyboard();
  },
  methods: {
    infoFromKeyCode(keyCode) {
      switch (keyCode) {
        case "Escape": return { key: "Escape", x: 0, y: 0 }

        case "F1": return { key: "F1", x: 2, y: 0 }
        case "F2": return { key: "F2", x: 3, y: 0 }
        case "F3": return { key: "F3", x: 4, y: 0 }
        case "F4": return { key: "F4", x: 5, y: 0 }
        case "F5": return { key: "F5", x: 6, y: 0 }
        case "F6": return { key: "F6", x: 7, y: 0 }
        case "F7": return { key: "F7", x: 8, y: 0 }
        case "F8": return { key: "F8", x: 9, y: 0 }
        case "F9": return { key: "F9", x: 10, y: 0 }
        case "F10": return { key: "F10", x: 11, y: 0 }
        case "F11": return { key: "F11", x: 12, y: 0 }
        case "F12": return { key: "F12", x: 13, y: 0 }

        case "Backquote": return { key: "Backquote", x: 0, y: 2 }
        case "Digit1": return { key: "Digit1", x: 1, y: 2 }
        case "Digit2": return { key: "Digit2", x: 2, y: 2 }
        case "Digit3": return { key: "Digit3", x: 3, y: 2 }
        case "Digit4": return { key: "Digit4", x: 4, y: 2 }
        case "Digit5": return { key: "Digit5", x: 5, y: 2 }
        case "Digit6": return { key: "Digit6", x: 6, y: 2 }
        case "Digit7": return { key: "Digit7", x: 7, y: 2 }
        case "Digit8": return { key: "Digit8", x: 8, y: 2 }
        case "Digit9": return { key: "Digit9", x: 9, y: 2 }
        case "Digit0": return { key: "Digit0", x: 10, y: 2 }
        case "Minus": return { key: "Minus", x: 11, y: 2 }
        case "Equal": return { key: "Equal", x: 12, y: 2 }
        case "Backspace": return { key: "Backspace", x: 13, y: 2 }

        case "Tab": return { key: "Tab", x: 0, y: 3 }
        case "KeyQ": return { key: "KeyQ", x: 1, y: 3 }
        case "KeyW": return { key: "KeyW", x: 2, y: 3 }
        case "KeyE": return { key: "KeyE", x: 3, y: 3 }
        case "KeyR": return { key: "KeyR", x: 4, y: 3 }
        case "KeyT": return { key: "KeyT", x: 5, y: 3 }
        case "KeyY": return { key: "KeyY", x: 6, y: 3 }
        case "KeyU": return { key: "KeyU", x: 7, y: 3 }
        case "KeyI": return { key: "KeyI", x: 8, y: 3 }
        case "KeyO": return { key: "KeyO", x: 9, y: 3 }
        case "KeyP": return { key: "KeyP", x: 10, y: 3 }
        case "BracketLeft": return { key: "BracketLeft", x: 11, y: 3 }
        case "BracketRight": return { key: "BracketRight", x: 12, y: 3 }
        case "Backslash": return { key: "Backslash", x: 13, y: 3 }
        
        case "CapsLock": return { key: "CapsLock", x: 0, y: 4 }
        case "KeyA": return { key: "KeyA", x: 1, y: 4 }
        case "KeyS": return { key: "KeyS", x: 2, y: 4 }
        case "KeyD": return { key: "KeyD", x: 3, y: 4 }
        case "KeyF": return { key: "KeyF", x: 4, y: 4 }
        case "KeyG": return { key: "KeyG", x: 5, y: 4 }
        case "KeyH": return { key: "KeyH", x: 6, y: 4 }
        case "KeyJ": return { key: "KeyJ", x: 7, y: 4 }
        case "KeyK": return { key: "KeyK", x: 8, y: 4 }
        case "KeyL": return { key: "KeyL", x: 9, y: 4 }
        case "Semicolon": return { key: "Semicolon", x: 10, y: 4 } 
        case "Quote": return { key: "Quote", x: 11, y: 4 }
        case "Enter": return { key: "Enter", x: 12, y: 4 }

        case "ShiftLeft": return { key: "ShiftLeft", x: 0, y: 5 }
        case "KeyZ": return { key: "KeyZ", x: 1, y: 5 }
        case "KeyX": return { key: "KeyX", x: 2, y: 5 }
        case "KeyC": return { key: "KeyC", x: 3, y: 5 }
        case "KeyV": return { key: "KeyV", x: 4, y: 5 }
        case "KeyB": return { key: "KeyB", x: 5, y: 5 }
        case "KeyN": return { key: "KeyN", x: 6, y: 5 }
        case "KeyM": return { key: "KeyM", x: 7, y: 5 }
        case "Comma": return { key: "Comma", x: 8, y: 5 }
        case "Period": return { key: "Period", x: 9, y: 5 }
        case "Slash": return { key: "Slash", x: 10, y: 5 }
        case "ShiftRight": return { key: "ShiftRight", x: 11, y: 5 }
 
        case "ControlLeft": return { key: "ControlLeft", x: 0, y: 7 }
        case "AltLeft": return { key: "AltLeft", x: 1, y: 7 }
        case "AltRight": return { key: "AltRight", x: 2, y: 7 }
        case "ControlRight": return { key: "ControlRight", x: 3, y: 7 }

        case "Space": return { key: "Space", x: 5, y: 7 }
        
        case "Insert": return { key: "Insert", x: 15, y: 3 }
        case "Delete": return { key: "Delete", x: 15, y: 4 }
        case "ScrollLock": return { key: "ScrollLock", x: 16, y: 2 }
        case "Home": return { key: "Home", x: 16, y: 3 }
        case "End": return { key: "End", x: 16, y: 4 }
        case "Pause": return { key: "Pause", x: 17, y: 2 }
        case "PageUp": return { key: "PageUp", x: 17, y: 3 }
        case "PageDown": return { key: "PageDown", x: 17, y: 4 }
        
        case "ArrowLeft": return { key: "ArrowLeft", x: 15, y: 7 }
        case "ArrowUp": return { key: "ArrowUp", x: 16, y: 6 }
        case "ArrowDown": return { key: "ArrowDown", x: 16, y: 7 }
        case "ArrowRight": return { key: "ArrowRight", x: 17, y: 7 }

        case "Numpad7": return { key: "Numpad7", x: 19, y: 2 }
        case "Numpad8": return { key: "Numpad8", x: 20, y: 2 }
        case "Numpad9": return { key: "Numpad9", x: 21, y: 2 }
        case "NumpadAdd": return { key: "NumpadAdd", x: 22, y: 2 }
        case "NumpadAdd": return { key: "NumpadAdd", x: 22, y: 2 }
        case "Numpad4": return { key: "Numpad4", x: 19, y: 3 }
        case "Numpad5": return { key: "Numpad5", x: 20, y: 3 }
        case "Numpad6": return { key: "Numpad6", x: 21, y: 3 }
        case "NumpadSubtract": return { key: "NumpadSubtract", x: 22, y: 3 }
        case "Numpad1": return { key: "Numpad1", x: 19, y: 4 }
        case "Numpad2": return { key: "Numpad2", x: 20, y: 4 }
        case "Numpad3": return { key: "Numpad3", x: 21, y: 4 }
        case "NumpadMultiply": return { key: "NumpadMultiply", x: 22, y: 4 }
        case "Numpad0": return { key: "Numpad0", x: 20, y: 5 }
        case "NumpadDecimal": return { key: "NumpadDecimal", x: 21, y: 5 }
        case "NumpadDivide": return { key: "NumpadDivide", x: 22, y: 5 }

        default: return undefined
      }
    },
    setupKeyboard() {
      const sections = document.getElementsByClassName("key-section");
      Array.from(sections).forEach((e, _) => { e.remove() });
      
      const width = 24;
      const Map2DTo1D = (x, y) => y * width + x;

      // create map of used keys
      let keyPool = this.isShowingFull ? allKeys : this.keys;
      let keyMap = []
      for (const key of keyPool) {
        let loc = this.infoFromKeyCode(key);
        keyMap[Map2DTo1D(loc.x, loc.y)] = { key: key, ...loc };
      }

      // create empty array to store each island of keys
      let keyIslands = [];

      // treat arrow keys specially:
      //    If you have left and right, but not up and down, then while left and right 
      //    are technically seperated on the map, they should remain grouped together.
      { 
        let arrowIsland = [];

        for (let name of ["ArrowUp", "ArrowDown", "ArrowLeft", "ArrowRight"]) {
          if (this.keys.includes(name)) {
            let key = this.infoFromKeyCode(name);
            keyMap[Map2DTo1D(key.x, key.y)] = 0;
            arrowIsland.push(key);
          }
        }

        if (arrowIsland.length > 0) {
          keyIslands.push(arrowIsland);
        }
      }

      // while there are unaccounted keys in the map...
      for (let first; first = keyMap.find(k => k); ) {
        // Create queue of searched keys
        let bfsQueue = [first];
        keyMap[Map2DTo1D(first.x, first.y)] = 0;
        
        // create empty array to store keys in this island
        let island = [];

        // while the queue isn't empty...
        for (let key; key = bfsQueue.shift(); ) {
          island.push(key);

          // for all surrounding keys...
          for (let x = -1; x < 2; x++) {
            for (let y = -1; y < 2; y++) {
              let neighbor = keyMap[Map2DTo1D(key.x + x, key.y + y)];
              // if the neighbor exists...

              if(neighbor) {
                console.log(`${key.key} -> ${neighbor.key}`)
                // add the neighbor to the queue so it's neighbors can be checked              
                bfsQueue.push(neighbor);

                // mark the key as counted on the map
                keyMap[Map2DTo1D(neighbor.x, neighbor.y)] = 0;
              }
            }
          }
        }
        keyIslands.push(island);
      }
      
      for (let island of keyIslands) {
        let section = document.createElement('div');
        section.classList.add('key-section');
        
        // get bounds for each island
        let minX = Number.MAX_VALUE, minY = Number.MAX_VALUE, maxX = 0;
        for (let key of island) {
          minX = Math.min(minX, key.x);
          maxX = Math.max(maxX, key.x);
          minY = Math.min(minY, key.y);
        }

        const keyPadding = 2;
        let sectionWidth = maxX - minX + 1
        let keyWidth;
        if (!this.isShowingFull) {
          keyWidth = this.width / Math.max(sectionWidth + 1, 6) - (2*keyPadding);
        }
        else {
          keyWidth = this.width / 16;
        }

        // set section width
        section.style.gridTemplateColumns = `repeat(${sectionWidth}, auto)`

        // create each key and assign position within its section
        const keyClass = Vue.extend(KeyButton);
        for (let key of island) {
          let keyElement = new keyClass({
            propsData: {
              keyCode: key.key,
              player: this.player,
              buttonSize: keyWidth,
              location: { x: key.x - minX, y: key.y - minY}
            }
          });
          keyElement.$mount();
          section.appendChild(keyElement.$el);
        }

        document.getElementById("keyboard-wrapper").appendChild(section);
      }
    }
  },
  data() {
    return {
      isShowingFull: false
    };
  },
  computed: {
    cssProps() {
      return {
        'width': `${this.width}px`
      };
    }
  }
}

</script>

<style>
.key-section {
  display: inline-grid;
  margin: 10px;
}

#keyboard-wrapper {
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
  align-items: center;
}

#show-keyboard {
  background-color: #9be24a;
  border: none;
  color: white;
  font-size: 20px;
  margin-left: 20px;
  padding: 5px;
}

#show-keyboard:active {
  filter: brightness(.85);
}

</style>
