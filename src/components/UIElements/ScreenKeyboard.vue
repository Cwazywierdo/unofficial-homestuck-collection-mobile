<template>
  <div>
    <div class="key-section">
      <KeyButton v-for="k in keys" :keyCode="k" :player="player" :buttonSize="50"></KeyButton>
    </div>
  </div>
</template>

<script>
import KeyButton from '@/components/UIElements/KeyButton.vue'

export default {
  components: { KeyButton },
  props: ["player", "keys"],
}

</script>

<style scoped>
.key-section {
  background-color: lightblue;
  display: inline-grid;
  grid-template-columns: repeat(2, auto);
}

</style>
