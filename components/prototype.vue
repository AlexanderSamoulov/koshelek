<template>
  <div>
    <b>{{ wsState }}</b>
    <span>{{ string }}</span>
    <button @click="subscribe" class="btn">Подписаться</button>
    <button @click="unSubscribe" class="btn">Отписаться</button>
    <button @click="closeWs" class="btn">Отключить</button>
  </div>
</template>

<script setup lang="ts">
const id = Math.floor(Math.random() * 1000);
const SUBSCRIBE = {
  method: "SUBSCRIBE",
  params: ["btcusdt@aggTrade", "btcusdt@depth"],
  id: id,
};
const UNSUBSCRIBE = {
  method: "UNSUBSCRIBE",
  params: ["btcusdt@depth"],
  id: id,
};

let subscribe:any=null

/* import {socket} from './../public/ws' */

const url = "wss://stream.binance.com:443/ws";
const wsState = ref("Неподключен");
const string = ref("");
onMounted(() => {
    if (process.client){
 const socket = new WebSocket(url);
    socket.onopen = function (event) {
  wsState.value = "Подключен";}
  socket.onmessage = (event) => {
  string.value = event.data;
};
subscribe =()=> {
    socket.send(JSON.stringify(SUBSCRIBE));
}



  // Отправляем сообщение по WS
  // socket.send('тут должен быть понг');
};


})

/* 
socket.onmessage = (event) => {
  string.value = event.data;
};



const subscribe =()=> {
    socket.send(JSON.stringify(SUBSCRIBE));
}

const unSubscribe =()=> {
    socket.send(JSON.stringify(UNSUBSCRIBE));
}

const closeWs =()=> {
    socket.close();
} */












</script>

<style scoped>
.btn{
    width: 50px;
    height: 20px;
    border-radius: 5px;
    cursor: pointer;
    background-color: #5fb80c;
}
</style>
