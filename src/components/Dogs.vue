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

  methods: {
    addDog(){
      const exists = this.dogs.some(dog => dog.name === this.name);
      if (!exists) this.dogs = sortDogs(this.dogs.concat({name: this.name}));
      this.name = '';
    }
  }
}
</script>
