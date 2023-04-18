<script setup>
import { ref } from "vue";
//get username
const username = prompt("Informe seu usúario");

const items = ref([]),
  message_text = ref(''),
  errorMessage = ref(''),
  messages = ref(null);

function send_message() {
  if (message_text.value !== "") {
    items.value.push({
      message: 'teste',
      name: 'Atendente'
    }, {
      message: message_text.value,
      name: username,
    });
    message_text.value = "";
    errorMessage.value = "";


    setTimeout(() => {
      messages.value.scrollTop = messages.value.scrollHeight;
    }, 100);
  } else {
    errorMessage.value = "Informe uma mensagem válida!";
  }
}
</script>
  

<template>
  <header>
    <h2 class="mb-5 text-3xl font-semibold text-gray-700">Atendimento Online</h2>
  </header>
  <div class="messages" ref="messages">
    <div v-for="item in items" :class="[item.name == 'Atendente' ? 'receive' : 'sent']">
      <span>{{ item.name }}</span>
      <p>{{ item.message }}</p>
    </div>
  </div>
  <form @submit.prevent="send_message" method="get">
    <div class="footer">
      <input type="text" id="message_text" v-model="message_text" placeholder="Digite sua mensagem...">
      <button class="btn_enviar">Send</button>
    </div>
  </form>
</template>

<style scoped>
header,
.footer {
  background: rgba(0, 0, 0, 0.692);
  height: 3.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 1rem;
  border-radius: 0.2rem;
  color: white
}

.messages {
  display: flex;
  height: 100%;
  padding: 1rem;
  border-radius: 0.5rem;
  flex-direction: column;
  gap: 0.4rem;
  overflow: auto;
  scrollbar-width: none;
  scroll-behavior: smooth;
  hyphens: auto;
}

p,
span {
  margin: 0 0.5rem;
}

span {
  font-size: 10px;
  color: rgba(245, 245, 245, 0.705);
}

.receive {
  display: grid;
  background-color: rgba(69, 103, 141, 0.63);
  padding: 0.5rem 0.2rem;
  width: min(300px);
  overflow-wrap: anywhere;
  border-radius: 0rem 1rem 1rem 1rem;
}

.sent {
  display: grid;
  padding: 0.5rem 0.2rem;
  justify-items: end;
  align-self: flex-end;
  background-color: #8ac1e0;
  width: min(300px);
  overflow-wrap: anywhere;
  border-radius: 1rem 1rem 0rem 1rem;
}

#message_text {
  height: 2rem;
  width: 100%;
  margin: 0 0.5rem;
  border-radius: 1rem;
  border: none;
  padding: 5px;
}

.btn_enviar {
  height: 2rem;
  width: 5rem;
  border-radius: 1rem;
  border: none;
  font-size: 12px;
  background-color: #a4c9e8;
  box-shadow: 0 2px 0 rgba(69, 103, 141, 0.63);
}

.btn_enviar:hover {
  background: rgba(69, 103, 141, 0.63);
}

.btn_enviar:active {
  position: relative;
  top: 1px;
  box-shadow: none;
}
</style>
  
