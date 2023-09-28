<script>
import { mapState } from 'pinia'
import ListOfExcercises from './ListOfExcercises.vue'
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
  <div>
    <ListOfExcercises :excercises="excercises" />
  </div>
</template>
