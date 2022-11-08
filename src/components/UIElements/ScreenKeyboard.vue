<template>
  <div>
    <KeyButton v-for="k in keys" :keyCode="k" :player="player"></KeyButton>
  </div>
</template>

<script>
import KeyButton from '@/components/UIElements/KeyButton.vue'

export default {
  components: { KeyButton },
  props: ["player", "keys"],
}

</script>