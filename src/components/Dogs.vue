<template>
  <div class="dogs">
    <table v-if="dogs.length">
      <tr>
        <th> Name </th>
      </tr>
      <tr v-for="(dog, index) in dogs" :key="index">
        <td>{{ dog.name }}</td>
      </tr>
    </table>
    <div>
      <label>Name</label>
      <input type="text" v-model="name"/>
      <button @keypress.enter="addDog" @click="addDog">Add</button>
    </div>
  </div>
</template>

<script>

function sortDogs(dogs) {
 dogs.sort((dogA, dogB) => dogA.name.localeCompare(dogB.name))
 return dogs;
} 

export default {
  data(){
    return {
      dogs: [],
      name: ''
    }
  },
    mounted(){
    this.dogs=[{name: 'Juno'}, {name: 'Bob'}];
  },
  methods: {
    addDog(){
      const exists = this.dogs.some(dog => dog.name === this.name);
      if (!exists) this.dogs = sortDogs(this.dogs.concat({name: this.name}));
      this.name = '';
    },

  }
}
</script>

<style scoped>
button, input {
  border: solid gray 1px;
  border-radius: 4px;
  padding: 4px;
}
input {
  margin: 0 10px;
}
label {
  font-weight: bold;
}
table {
  border-collapse: collapse;
  margin-bottom: 10px;
}
td, th {
  border: solid gray 1px;
  padding: 5px;
}
</style>