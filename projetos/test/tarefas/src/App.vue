<template>
  <div>
    <div class="aFazer">
      <h1>Tarefas do dia.</h1>
      <div class="controles">
        <input class="inputTarefa" v-model="tarefa" placeholder="Sua tarefa">
        <button class="button" type="button" v-on:click="newTarefa()">Add</button>
      </div>
      <ul>
        <li v-for="(item, i) of list" :key="i">
          <h4>{{ item.title }}</h4>
          <button v-on:click="tarefaOk(i)">Finalizar tarefa</button>
          <button v-on:click="descTarefa(i)">Descartar tarefa</button>
        </li>
      </ul>
    </div>
    <div class="realizadas">
      <h1>Tarefas realizadas</h1>
      <ul>
        <li v-for="(item, i) of realizadas" :key="i">
          <h4>{{ item.title }}</h4>
          <p>{{ item.date }}</p>
        </li>
      </ul>
    </div>
    <div class="descartadas">
      <h1>tarefas descartadas</h1>
      <ul>
        <li v-for="(item, i) of descartadas" :key="i">
          <h4>{{ item.title }}</h4>
          <p>{{ item.date }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
const moment = require('moment');
export default {
  data () {
    return {
      tarefa: '',
      list: [],
      realizadas: [],
      descartadas: [],
    }
  },

  methods: {
    newTarefa: function() {
      let tarefa = this.tarefa;
      this.list.push({title: tarefa});
      tarefa = ''
    },

    tarefaOk: function(index) {
      let lista = this.list;
      let realizada = this.realizadas;

      const title = lista[index].title

      realizada.push({title: title, date: moment().format('DD-MM-YYYY HH:mm:ss') });

      lista.splice(index, 1);
    },

    descTarefa: function(index) {
      let lista = this.list;
      let descartada = this.descartadas;

      const title = lista[index].title

      descartada.push({title: title, date: moment().format('DD-MM-YYYY HH:mm:ss') });
      
      lista.splice(index, 1);
    },
  }
}
</script>

<style lang="scss">

body{
  background-color: #6C767E;
  display: flex;
  justify-content: center;
}

li{
  list-style-type: none;
  display: flex;
  flex-direction: row;
  background-color: #37B0E8;
  width: 96%;
  justify-content: space-around;
  margin-bottom: 20px;
  border-radius: 6px;
  align-items: center;
}

li h4 {
  color: #2C3034;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 25px;
  margin: 10px;
}

li button {
  height: 80%;
  margin-left: 45px;
  font-size: 24px;
  border-radius: 4px;
  border: 1px, solid, none;
  font-family: Arial, Helvetica, sans-serif;
}

li p {
  color: #2C3034;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 24px;
}

.aFazer{
  background-color: #2C3034;
  width: 90vw;
  border-radius: 8px;
  padding-bottom: 5px;
}

.aFazer h1 {
  font-size: 60px;
  color: #FFFF;
  font-family: Arial, Helvetica, sans-serif;
  margin-top: 4%;
  margin-left: 8%;
}

.controles {
  display: flex;
}

.inputTarefa {
  height: 50px;
  width: 70%;
  border-radius: 8px;
  margin: 4%;
  font-size: 35px;
}

.button {
  background-color: #37B0E8;
  color:#2C3034;
  height: 50px;
  width: 18%;
  margin-top: 40px;
  border-radius: 8px;
  font-size: 35px;
}

.descartadas{
  background-color: #2C3034;
  width: 90vw;
  border-radius: 8px;
  padding-bottom: 5px;
}

.descartadas h1 {
  font-size: 60px;
  color: #FFFF;
  font-family: Arial, Helvetica, sans-serif;
  margin: 4%;
  margin-left: 8%;
}

.realizadas{
  background-color: #2C3034;
  width: 90vw;
  border-radius: 8px;
  padding-bottom: 5px;
}

.realizadas h1 {
  font-size: 60px;
  color: #FFFF;
  font-family: Arial, Helvetica, sans-serif;
  margin: 4%;
  margin-left: 8%;
}
</style>
