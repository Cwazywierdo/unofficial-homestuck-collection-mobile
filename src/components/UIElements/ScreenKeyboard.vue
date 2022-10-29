<template>
  <div>
    <KeyButton keyCode="KeyW" :player="player"/>
    <KeyButton keyCode="KeyA" :player="player"/>
    <KeyButton keyCode="KeyS" :player="player"/>
    <KeyButton keyCode="KeyD" :player="player"/>
    <KeyButton keyCode="Space" :player="player"/>
  </div>
</template>

<script>
import KeyButton from '@/components/UIElements/KeyButton.vue'

export default {
  components: { KeyButton },
  props: ["player"]
}

</script>