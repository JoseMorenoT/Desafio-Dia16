<template>
    <div id="scrollableDiv" class="container bg-rgb-custom border border-dark">
      <div v-for="(mensaje, index) in mensajes" :key="index">
        <p :style="{textAlign: mensaje.id === usuarios[0].id.value? 'left' : 'right',}"><small>{{ mensaje.nombreCompleto }}</small></p>
        <p :style="{backgroundColor: mensaje.color,textAlign: mensaje.id === usuarios[0].id.value? 'left' : 'right',}">{{ mensaje.texto }}</p>
      </div>
    </div>
  </template>
  <script>
export default {
  name: "ChatPeople",
  props: {
    mensajes: Array,
    usuarios: Array,
  },
};
</script>
  
<style scoped>
#scrollableDiv {
  max-height: 80vh;
  overflow-y: scroll;
}
.bg-rgb-custom {
  background-color: rgb(210, 210, 186);
}
</style>