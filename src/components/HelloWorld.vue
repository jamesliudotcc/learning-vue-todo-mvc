<template>
  <div class="hello">
    <input v-model="draftToDo">
    {{draftToDo}}
    <br>
    <button v-on:click="addToDo">Add to do</button>
    <button v-on:click="clearDone">Clear Done</button>
    <p>
      <input type="radio" name="isDone" id="all" checked v-on:click="changeShow('all')">
      <label for="all">All</label>
      <input type="radio" name="isDone" id="done" v-on:click="changeShow('done')">
      <label for="done">Done</label>
      <input type="radio" name="isDone" id="undone" v-on:click="changeShow('undone')">
      <label for="undone">Not Done</label>
    </p>
    <!-- TODO: refactor to pass as props intead of hardcoding -->
    <ul v-if="show == 'all'">
      <li v-for="(toDo, index) in toDos" v-bind:key="index">
        <input type="checkbox" :name="index" :id="index" v-model="toDo.done">
        <label v-bind:class="{done:toDo.done}" :for="index">{{toDo.name}}</label>
      </li>
    </ul>
    <ul v-if="show == 'done'">
      <li v-for="(toDo, index) in doneToDos" v-bind:key="index">
        <input type="checkbox" :name="index" :id="index" v-model="toDo.done">
        <label v-bind:class="{done:toDo.done}" :for="index">{{toDo.name}}</label>
      </li>
    </ul>
    <ul v-if="show == 'undone'">
      <li v-for="(toDo, index) in undoneToDos" v-bind:key="index">
        <input type="checkbox" :name="index" :id="index" v-model="toDo.done">
        <label v-bind:class="{done:toDo.done}" :for="index">{{toDo.name}}</label>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data: function() {
    return { draftToDo: '', toDos: [], show: 'all' };
  },
  computed: {
    doneToDos: function() {
      return this.toDos.filter(toDo => toDo.done);
    },
    undoneToDos: function() {
      return this.toDos.filter(toDo => !toDo.done);
    },
  },
  methods: {
    addToDo: function() {
      if (this.draftToDo == '') {
        return;
      }
      this.toDos.push({ name: this.draftToDo, done: false });
      this.draftToDo = '';
    },
    changeShow: function(what) {
      console.log(what);
      this.show = what;
    },
    clearDone: function() {
      this.toDos = this.toDos.filter(toDo => !toDo.done);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
a {
  color: #42b983;
}
.done {
  text-decoration: line-through;
}
</style>
