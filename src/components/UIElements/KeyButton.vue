<template>
  <button @mousedown="clicked" @mouseup="released" @mouseleave="released">{{ labelFromKeyCode() }}</button>
</template>

<script>
export default{
  name: "KeyButton",
  props: ['keyCode', 'player'],
  mounted() {
    
  },
  methods: {
    labelFromKeyCode() {
      switch (this.keyCode) {
        case "Backspace": return "BKSP"
        case "Tab": return "Tab"
        case "Enter": return "Enter"
        case "ShiftLeft":
        case "ShiftRight": return "Shift"
        case "ControlLeft":
        case "ControlRight": return "Ctrl"
        case "AltLeft":
        case "AltRight": return "Alt"
        case "CapsLock": return "Caps"
        case "Escape": return "Esc"
        case "Space": return "Space"
        case "Digit0": return "0"
        case "Digit1": return "1"
        case "Digit2": return "2"
        case "Digit3": return "3"
        case "Digit4": return "4"
        case "Digit5": return "5"
        case "Digit6": return "6"
        case "Digit7": return "7"
        case "Digit8": return "8"
        case "Digit9": return "9"
        case "KeyA": return "A"
        case "KeyB": return "B"
        case "KeyC": return "C"
        case "KeyD": return "D"
        case "KeyE": return "E"
        case "KeyF": return "F"
        case "KeyG": return "G"
        case "KeyH": return "H"
        case "KeyI": return "I"
        case "KeyJ": return "J"
        case "KeyK": return "K"
        case "KeyL": return "L"
        case "KeyM": return "M"
        case "KeyN": return "N"
        case "KeyO": return "O"
        case "KeyP": return "P"
        case "KeyQ": return "Q"
        case "KeyR": return "R"
        case "KeyS": return "S"
        case "KeyT": return "T"
        case "KeyU": return "U"
        case "KeyV": return "V"
        case "KeyW": return "W"
        case "KeyX": return "X"
        case "KeyY": return "Y"
        case "KeyZ": return "Z"
        case "Semicolon": return ";"
        case "Equal": return "="
        case "Comma": return ","
        case "Minus": return "-"
        case "Period": return "."
        case "Slash": return "/"
        case "Backquote": return "`"
        case "BracketLeft": return "["
        case "Backslash": return "\\"
        case "BracketRight": return "]"
        case "Quote": return "'"
        case "Numpad0": return "0"
        case "Numpad1": return "1"
        case "Numpad2": return "2"
        case "Numpad3": return "3"
        case "Numpad4": return "4"
        case "Numpad5": return "5"
        case "Numpad6": return "6"
        case "Numpad7": return "7"
        case "Numpad8": return "8"
        case "Numpad9": return "9"
        case "NumpadMultiply": return "*"
        case "NumpadAdd": return "+"
        case "NumpadSubtract": return "-"
        case "NumpadDecimal": return "."
        case "NumpadDivide": return "/"
        case "PageUp": return "Pg Up"
        case "PageDown": return "Pg Dwn"
        case "End": return "End"
        case "Home": return "Home"
        case "ArrowLeft": return "Left"
        case "ArrowUp": return "Up"
        case "ArrowRight": return "Right"
        case "ArrowDown": return "Down"
        case "Insert": return "Ins"
        case "Delete": return "Del"
        case "Pause": return "Pause"
        case "ScrollLock": return "Lock"
        case "F1": return "F1"
        case "F2": return "F2"
        case "F3": return "F3"
        case "F4": return "F4"
        case "F5": return "F5"
        case "F6": return "F6"
        case "F7": return "F7"
        case "F8": return "F8"
        case "F9": return "F9"
        case "F10": return "F10"
        case "F11": return "F11"
        case "F12": return "F12"
        default: return undefined
      }
    },
    
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
  }
}
</script>