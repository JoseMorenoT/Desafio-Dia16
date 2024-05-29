<template>
  <div id="app">
    <main class="my-5 container">
      <div class="row">
        <div class="col-3">
          <CardPerson
            :usuario="usuarios[0]"
            @enviarMensaje="enviarMensajeHandler"
          />
        </div>
        <div class="col-6 d-flex">
          <ChatPeople :mensajes="mensajes" :usuarios="usuarios" />
        </div>
        <div class="col-3">
          <CardPerson
            :usuario="usuarios[1]"
            @enviarMensaje="enviarMensajeHandler"
          />
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import axios from "axios";
import CardPerson from "./components/CardPerson.vue";
import ChatPeople from "./components/ChatPeople.vue";

export default {
  name: "App",
  components: {
    CardPerson,
    ChatPeople,
  },
  data() {
    return {
      usuarios: [],
      mensajes: [],
    };
  },
  // Llamado del API
  methods: {
    async getPerson() {
      try {
        let response = await axios.get("https://randomuser.me/api/?results=2");
        this.usuarios = response.data.results;
        console.log(response);
      } catch (error) {
        console.log(error);
      }
    },
    enviarMensajeHandler(mensaje) {
      let nuevoMensaje = {
        id: mensaje.id,
        color: mensaje.color,
        nombreCompleto: mensaje.nombreCompleto,
        texto: mensaje.texto,
      };
      this.mensajes.push(nuevoMensaje);
    },
  },
  // metodo de ciclo, digo a app.vue, apenas me monte al DOM ejecute la funcion getPerson
  mounted() {
    this.getPerson();
  },
};
</script>

<style scoped>
* {
  font-family: "Roboto", sans-serif;
  font-weight: 400;
}
</style>
