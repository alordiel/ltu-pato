<script>
import { mapState } from 'pinia'
import { useExcercisesStore } from '@/stores/excercises'

export default {

  components: {
  },
  created(){
    const currentID = this.$route.params.id;
        console.log(currentID)
        const index = this.excercises.findIndex(e => e.id === currentID);
        this.currentExcercise = this.excercises[index];
    
  },
  data() {
    return {
        currentExcercise: {},
    }
  },
  computed: {
    ...mapState(useExcercisesStore, ['excercises']),
   
  },
  methods: {
   
  }
}

</script>


<template>
    <main class="single-excercise">
        <h1 class="text-center">{{ currentExcercise.title }}</h1>
        <h2 class="text-center">{{ currentExcercise.subtitle }}</h2>
    </main>
</template>

<style>
@media (min-width: 1024px) {
  .single-excercise {
    min-height: calc(100vh - 125px);
  }
}
</style>
