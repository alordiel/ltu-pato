<script>
import { mapState } from 'pinia'
import ExcerciseExam from '../components/ExcerciseExam.vue';
import { useExcercisesStore } from '@/stores/excercises'

export default {

  components: {
    ExcerciseExam,
  },
  created(){
    const currentID = this.$route.params.id;
    const index = this.excercises.findIndex(e => e.id === currentID);
    this.currentExcercise = this.excercises[index];
    this.mode = 'main';
  },
  data() {
    return {
        currentExcercise: {},
        mode: 'main',
    }
  },
  computed: {
    ...mapState(useExcercisesStore, ['excercises']),
  },
}

</script>


<template>
    <main class="single-excercise">
        <h1 class="text-center">{{ currentExcercise.title }}</h1>
        <h2 class="text-center">{{ currentExcercise.subtitle }}</h2>
        <div v-show="mode === 'main'">
            <div class="excercise-options">
                <p class="text-center" style="width:100%">Изберете режим</p>
                <button @click="mode = 'learning'">Обучение</button>
                <button @click="mode = 'test'">Тест</button>
            </div>
        </div>
        <div v-show="mode==='learning'">
            <div class="back-to-option">
                <button @click="mode = 'main'">Назад</button>
            </div>
            <div class="learning-mode">
                <div class="image" v-for="(image, key) in currentExcercise.images" :key="'img-' + key">
                    <figure>
                        <img :src="'/pato/images/thumbnails/'+image.filename" :alt="image.name" width="300">
                        <figcaption>{{ image.name }}</figcaption>
                    </figure>
                </div>
            </div>
        </div>
        <div v-if="mode === 'test'">
            <ExcerciseExam :images="currentExcercise.images"></ExcerciseExam>
        </div>
    </main>
</template>

<style>
.excercise-options {
    max-width: 300px;
    margin: 20px auto;
    border: 1px #fff solid;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
}
.excercise-options button {
    width: 90px;
    text-align: center;
    font-weight: bold;
    border: 1px #eee solid;
    border-radius: 5px;
    padding: 5px 10px;
    margin: 15px 10px;
    cursor: pointer;
}

@media (min-width: 1024px) {
  .single-excercise {
    min-height: calc(100vh - 125px);
  }
}
</style>
