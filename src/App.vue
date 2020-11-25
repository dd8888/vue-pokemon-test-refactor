<template>
  <div>
    <PokeCard :index="32" />
  </div>
</template>

<script>
import PokeCard from './components/PokeCard'

export default {
  name: 'App',
  components: {
    PokeCard
  }
}
</script>

<style></style>
