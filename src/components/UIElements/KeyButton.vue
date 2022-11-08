<template>
  <button :style="cssProps" @mousedown="clicked" @mouseup="released" @mouseleave="released">{{ infoFromKeyCode.name }}</button>
</template>

<script>
export default{
  name: "KeyButton",
  props: ['keyCode', 'player', 'buttonSize'],
  mounted() {
    
  },
  methods: {
    CREvent(eventType) {
      // ruffle needs to be clicked into focus to register keyboard events
      let pointerEvent = new PointerEvent("pointerdown");
      this.player.dispatchEvent(pointerEvent);

      var e = new Event(eventType);
      e.key = "";
      e.code = this.keyCode;
      window.dispatchEvent(e);
    },
    clicked() { this.CREvent("keydown") },
    released() { this.CREvent("keyup") }
  },
  computed: {
    infoFromKeyCode() {
      switch (this.keyCode) {
        case "Escape": return { name: "Esc", location: { x: 0, y: 0 }, width: 2.5 }

        case "F1": return { name: "F1", width: 2 }
        case "F2": return { name: "F2", width: 2 }
        case "F3": return { name: "F3", width: 2 }
        case "F4": return { name: "F4", width: 2 }
        case "F5": return { name: "F5", width: 2 }
        case "F6": return { name: "F6", width: 2 }
        case "F7": return { name: "F7", width: 2 }
        case "F8": return { name: "F8", width: 2 }
        case "F9": return { name: "F9", width: 2 }
        case "F10": return { name: "F10", width: 2.5 }
        case "F11": return { name: "F11", width: 2.5 }
        case "F12": return { name: "F12", width: 2.5 }        

        case "Backquote": return { name: "`" }
        case "Digit1": return { name: "1" }
        case "Digit2": return { name: "2" }
        case "Digit3": return { name: "3" }
        case "Digit4": return { name: "4" }
        case "Digit5": return { name: "5" }
        case "Digit6": return { name: "6" }
        case "Digit7": return { name: "7" }
        case "Digit8": return { name: "8" }
        case "Digit9": return { name: "9" }
        case "Digit0": return { name: "0" }
        case "Minus": return { name: "-" }
        case "Equal": return { name: "=" }
        case "Backspace": return { name: "Back", width: 3.5 }

        case "Tab": return { name: "Tab", width: 3 }
        case "KeyQ": return { name: "Q" }
        case "KeyW": return { name: "W" }
        case "KeyE": return { name: "E" }
        case "KeyR": return { name: "R" }
        case "KeyT": return { name: "T" }
        case "KeyY": return { name: "Y" }
        case "KeyU": return { name: "U" }
        case "KeyI": return { name: "I" }
        case "KeyO": return { name: "O" }
        case "KeyP": return { name: "P" }
        case "BracketLeft": return { name: "[" }
        case "BracketRight": return { name: "]" }
        case "Backslash": return { name: "\\" }
        
        case "CapsLock": return { name: "Caps", width: 3 }
        case "KeyA": return { name: "A" }
        case "KeyS": return { name: "S" }
        case "KeyD": return { name: "D" }
        case "KeyF": return { name: "F" }
        case "KeyG": return { name: "G" }
        case "KeyH": return { name: "H" }
        case "KeyJ": return { name: "J" }
        case "KeyK": return { name: "K" }
        case "KeyL": return { name: "L" }
        case "Semicolon": return { name: ";" }
        case "Quote": return { name: "'" }
        case "Enter": return { name: "Enter", width: 4.5 }

        case "ShiftLeft": return { name: "L.Shift", width: 5.5 }
        case "KeyZ": return { name: "Z" }
        case "KeyX": return { name: "X" }
        case "KeyC": return { name: "C" }
        case "KeyV": return { name: "V" }
        case "KeyB": return { name: "B" }
        case "KeyN": return { name: "N" }
        case "KeyM": return { name: "M" }
        case "Comma": return { name: "," }
        case "Period": return { name: "." }
        case "Slash": return { name: "/" }
        case "ShiftRight": return { name: "R.Shift", width: 5.5 }

        case "ControlLeft": return { name: "L.Ctrl", width: 4.5 }
        case "AltLeft": return { name: "L.Alt", width: 3.5 }
        case "AltRight": return { name: "R.Alt", width: 3.5 }
        case "ControlRight": return { name: "R.Ctrl", width: 4.5 }

        case "Space": return { name: "Space", width: 2.3 }
        
        case "Insert": return { name: "Ins", width: 2.5 }
        case "Delete": return { name: "Del", width: 2.5 }
        case "ScrollLock": return { name: "Lock", width: 3 }
        case "Home": return { name: "Home", width: 3.5 }
        case "End": return { name: "End", width: 2.5 }
        case "Pause": return { name: "Pause", width: 4 }
        case "PageUp": return { name: "Pg Up", width: 4 }
        case "PageDown": return { name: "Pg Dwn", width: 4.5 }
        
        case "ArrowLeft": return { name: "Left", width: 3 }
        case "ArrowUp": return { name: "Up", width: 1.5 }
        case "ArrowDown": return { name: "Down", width: 3 }
        case "ArrowRight": return { name: "Right", width: 3.5 }

        case "Numpad7": return { name: "7" }
        case "Numpad8": return { name: "8" }
        case "Numpad9": return { name: "9" }
        case "NumpadAdd": return { name: "+" }
        case "Numpad4": return { name: "4" }
        case "Numpad5": return { name: "5" }
        case "Numpad6": return { name: "6" }
        case "NumpadSubtract": return { name: "-" }
        case "Numpad1": return { name: "1" }
        case "Numpad2": return { name: "2" }
        case "Numpad3": return { name: "3" }
        case "NumpadMultiply": return { name: "*" }
        case "Numpad0": return { name: "0" }
        case "NumpadDecimal": return { name: "." }
        case "NumpadDivide": return { name: "/" }

        default: return undefined
      }
    },
    cssProps() {
      return {
        '--text-scalar': `${ this.infoFromKeyCode.width != null ? ( 1 / this.infoFromKeyCode.width) : 1 }`,
        '--button-size': `${this.buttonSize}px`
      }
    }
  }
}
</script>

<style>  
  button {
    width: var(--button-size);
    height: var(--button-size);
    --margin: 2px;
    background-color: #4ae24d;
    border: none;
    color: white;
    font-size: calc((var(--button-size) - (var(--margin) * 2)) * var(--text-scalar) * .75);
    margin: var(--margin);
    font-weight: bold;
    white-space: break-spaces;
    padding: 2px;
    display:block;
    text-align: center;
  }

  button:active:hover {
    background-color: #3ebe40;
  }
</style>
