<template>
  <div id="app">
    <!--El v-if permite asegurar que la información de ambos user este disponible antes de mostrar la interfaz-->
    <div class="chat-container" v-if="user1 && user2">
      <!--Componente hijo que representa a usuario1 de chat y al mensaje que se agregará-->
      <UsuarioComponent :user="user1" @enviar-mensaje="agregarMensaje" />
      <!--Componente hijo que muestra los mensajes del chat-->
      <MensajesChat :mensajes="mensajes" :user1="user1" />
      <!--Componente hijo que representa a usuario2 de chat. Método que añade los mensajes al chat, ademas de integrar una 
      propiedad adicional para el valor del color incial del usuario-->
      <UsuarioComponent :user="user2" :color-inicial="'#FFFEFA'" @enviar-mensaje="agregarMensaje" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import MensajesChat from './components/MensajesChat.vue';
import UsuarioComponent from './components/UsuarioComponent.vue';

export default {
  name: 'App',
  components: {
    UsuarioComponent,
    MensajesChat,
  },
  data() {
    //Retorna un array de mensajes del chat, un objeto por cada usuario inicialmente nulo //
    return {
      mensajes: [],
      user1: null,
      user2: null,
    };
  },
  mounted() {
    // Ciclo de vida que llama al método fetch para obtener los datos del los users//
    this.fetchUsers();
  },
  methods: {
    //Método asíncrono que permite obtener datos de los users utilizando axios//
    async fetchUsers() {
      try {
        // Hace solicitudes a la HTTP para obtener dos users diferentes aleatorios//
        const response1 = await axios.get('https://randomuser.me/api/');
        const response2 = await axios.get('https://randomuser.me/api/');
        //Asigna una respuesta a dos user //
        this.user1 = response1.data.results[0];
        this.user2 = response2.data.results[0];
      } catch (error) {
        console.error('Error fetching users:', error);
      }
    },
    //Método que toma como argumento user, mensaje y color//
    agregarMensaje({ user, mensaje, color }) {
      //Agrega los objetos del array//
      this.mensajes.push({ user, text: mensaje, color });
    },
  },
};
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  font-family: Arial, sans-serif;
}

.message-inputs {
  display: flex;
  justify-content: space-between;
  width: 100%;
}

.chat-container {
  display: flex;

}
</style>
