<template>
  <div class="container">
    <h1>{{ name }}</h1>
    <img :src="imgUrl" :alt="name" />
    <span class="weight">{{ weight }}</span>
    <span class="height">{{ height }}</span>
    <span class="type" v-for="(type, index) in types" :key="index">{{
      type.type.name
    }}</span>
  </div>
</template>

<script>
const URL = 'https://pokeapi.co/api/v2/pokemon/'
const MAX = 152
const MIN = 0
export default {
  name: 'Pokecard',
  props: {
    index: {
      type: Number,
      required: true,
      validator: (v) => v >= MIN && v <= MAX

    }
  },
  data: function () {
    return {
      name: '',
      weight: 0,
      height: 0,
      imgUrl: '',
      types: []
    }
  },
  methods: {
    fetchData () {
      return fetch(URL + this.index)
        .then(response => response.json())
        .then(data => data)
    }
  },
  mounted () {
    this.fetchData().then(data => {
      console.log(data)
      this.name = data.name.charAt(0).toUpperCase() + data.name.slice(1)
      this.weight = data.weight
      this.height = data.height
      this.imgUrl =
        data.sprites.versions['generation-iv'].platinum.front_default
      this.types = data.types
    })
  }
}
</script>

<style>
h1 {
  background-color: green;
  color: white;
  border: 1px solid black;
  box-shadow: 2px 2px 5px grey;
  border-radius: 5px;
  width: 75px;
  font-size: 1em;
  text-transform: capitalize;
  margin: 3px;
}
.height {
  background-color: blue;
  color: white;
  padding: 0 10px;
}
.weight {
  background-color: red;
  color: white;
  padding: 0 10px;
}
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 128px;
  border: 2px solid black;
  box-shadow: 0 0 5px #666 inset;
}
img {
  width: 80px;
}
</style>
