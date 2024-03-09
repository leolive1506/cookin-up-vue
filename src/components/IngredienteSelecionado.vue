<script lang="ts">
import Tag from './Tag.vue'
export default {
  components: { Tag },
  props: {
    ingrediente: { type: String, required: true }
  },
  data() {
    return {
      selecionado: false
    }
  }
}
</script>

<template>
  <button
    class="ingrediente"
    @click="selecionado = !selecionado"
    :aria-pressed="selecionado"
  >
    <tag :texto="ingrediente" :isAtiva="selecionado"/>
  </button>
</template>
<style scoped>
.ingrediente {
  cursor: pointer
}
</style>