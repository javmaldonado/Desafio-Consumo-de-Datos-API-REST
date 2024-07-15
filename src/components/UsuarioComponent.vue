<template>
  <div class="user-container">
    <div class="user-info">
      <!-- Muestra la imagen mediante del objeto user -->
      <img :src="user.picture.large" class="user-image" alt="User" />
      <!-- Muestra el nombre  mediante del objeto user -->
      <div class="user-name">{{ user.name.first }} {{ user.name.last }}</div>
    </div>
    <!-- Prevent evita que la página se recargue, usa el método enviarForm para enviar el formulario -->
    <form @submit.prevent="enviarForm" class="mensajeForm">
      <!-- Permite que el usuario elija un color-->
      <input type="color" v-model="color" />
      <textarea v-model="mensaje"></textarea>
      <button type="submit">Enviar</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'UsuarioComponent',
  props: {
    // Las props define las PROPiedades que el componente espera recibir, en este caso espera un objeto que contentrá la información de user y una cadena color inicial //
    user: Object,
    colorInicial: String,
  },
  data() {
    // Retorna un objeto con el mensaje del user y el color que el usuario a elegido //
    return {
      mensaje: '',
      color: this.colorInicial || '#CBEAFF',
    };
  },
  methods: {
    //Emite un evento con un objeto compuesto por el user,mensaje y color //
    enviarForm() {
      if (this.mensaje) {
        this.$emit('enviar-mensaje', {
          user: this.user,
          mensaje: this.mensaje,
          color: this.color,
        });
        this.mensaje = '';
      }
    },
  },
};
</script>

<style>
.mensajeForm {
  width: 200px;
  display: flex;
  flex-direction: column;
  align-items: stretch;
}

textarea {
  width: 97%;
  height: 100px;
  margin-bottom: 10px;

}

button {

  width: 100%;
}

input {
  width: 100%;
  margin-bottom: 10px;

}

.user-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 50%;
}

.user-image {
  width: 200px;
  height: 200px;
}

.user-name {
  margin: 10px 0;
  font-weight: bold;

}
</style>
