<template>
  <div id="card__person" class="container">
    <div class="card">
      <img :src="usuario.picture.large" class="card-img-top" alt="" />
      <div class="card-body">
        <h5 class="card-title">
          {{ nombreCompleto }}
        </h5>
        <form>
          <input
            class="form-control my-2"
            type="color"
            name="color"
            id="color"
            v-model="mensaje.color"
          />
          <textarea
            class="form-control my-2"
            name="chat"
            id="chat"
            v-model="mensaje.texto"
            @keyup.enter="enviarMensaje"
          ></textarea>
          <br>
          <button @click.prevent="enviarMensaje" class="btn btn-info">Enviar</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardPerson",
  props: {
    usuario: Object,
  },
  data() {
    return {
      mensaje: {
        texto: "",
        color: "#fff",
        id: "",
      },
    };
  },
  computed: {
    nombreCompleto() {
      return `${this.usuario.name.first} ${this.usuario.name.last}`;
    },
  },
  methods: {
    enviarMensaje() {
      this.mensaje.id = this.usuario.id.value;
      this.mensaje.nombreCompleto = this.nombreCompleto;
      this.$emit("enviarMensaje", this.mensaje);
      this.mensaje.texto = "";
    },
  },
  created() {
    console.log(this.usuario);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  font-family: "Roboto", sans-serif;
  font-weight: 400;
}
textarea {
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 10px;
  font-size: 16px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  resize: none;
}

button {
  background-color: #128c7e;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 10px;
  cursor: pointer;
}

button:hover {
  background-color: #0d6e5b;
}
</style>
