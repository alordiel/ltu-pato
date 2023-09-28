<script>
import { mapState } from 'pinia'
import ListOfExcercises from '../components/ListOfExcercises.vue'
import { useExcercisesStore } from '@/stores/excercises'


export default {
  components: {
    ListOfExcercises
  },
  data() {
    return {
      bla:0,
    }
  },
  computed: {
    ...mapState(useExcercisesStore, ['excercises'])
  }
}
</script>
<template>
  <main>
    <h1>Упражнения по Патоморфология</h1>
    <h3>Изберете упражнение</h3>
    <ListOfExcercises :excercises="excercises" />
  </main>
</template>
