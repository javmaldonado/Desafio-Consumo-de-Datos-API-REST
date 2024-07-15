<template>
  <div class="ventana-chat">
    <!-- El v-for permite recorrer lista de mensajes y crear un bloque HTML -->
    <div v-for="(mensaje, index) in mensajes" :key="index">
      <!-- Aplica las clases dependiendo si es el usuario1 quien envia el mensaje -->
      <div
        :class="{ 'nombre-chat': true, 'nombre-usuario1': isUser1(mensaje.user), 'nombre-usuario2': !isUser1(mensaje.user) }">
        <!-- Permite mostrar el nombre de quien envió el mensaje -->
        <small>{{ mensaje.user.name.first }} {{ mensaje.user.name.last }}</small>
      </div>
      <!-- Con las clases dinamicas se puede definir cuando mostrar el contenedor-msg del user1 o el user2-->
      <div
        :class="{ 'contenedor-mensaje': true, 'contenedor-msg-usuario1': isUser1(mensaje.user), 'contenedor-msg-usuario2': !isUser1(mensaje.user) }">
        <!-- Con las clases dinamicas se puede definir cuando mostrar el mensaje del user1 o el user2-->
        <div
          :class="{ 'mensajes-chat': true, 'mensaje-usuario1': isUser1(mensaje.user), 'mensaje-usuario2': !isUser1(mensaje.user) }"
          :style="{ backgroundColor: mensaje.color }">
          {{ mensaje.text }}
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'MensajesChat',
  // Las props define las PROPiedades que el compomente espera recibir, en este caso espera un array que contentrá los mensajes y un objeto //
  props: {
    mensajes: Array,
    user1: Object,
  },
  // Define las funciones dentro del componente//
  methods: {
    // la funcion isUser1 se usa para verificar si cada mensaje fue enviado por user1 y de esta manera aplicar los estilos seleccionados por el user. //
    isUser1(user) {
      return user.name.first === this.user1.name.first && user.name.last === this.user1.name.last;
    }
  }
};
</script>

<style>
.ventana-chat {
  display: flex;
  flex-direction: column;
  width: 800px;
  max-height: 400px;
  overflow: auto;
  border: 1px solid #ccc;
  box-shadow: 5px 10px 18px #888888;
  padding: 10px;
  background-color: #EFE6DD;
}

.mensajes-chat {
  padding: 5px;
  margin: 2px;
  border-radius: 10px;
  word-break: break-all;
  word-wrap: break-word;
}

.contenedor-mensaje {
  display: flex;
  margin-bottom: 5px;
}

.contenedor-msg-usuario1 {
  justify-content: flex-start;
}

.contenedor-msg-usuario2 {
  justify-content: flex-end;
}

.nombre-chat {
  font-size: 10px;
  font-weight: lighter;
  color: #bfbbbbd2;

}

.nombre-usuario1 {
  text-align: left;
}

.nombre-usuario2 {
  text-align: right;
}

.mensaje-usuario1 {
  text-align: left;
  font-family: Georgia, 'Times New Roman', Times, serif
}

.mensaje-usuario2 {
  text-align: right;
  font-family: Georgia, 'Times New Roman', Times, serif
}
</style>
