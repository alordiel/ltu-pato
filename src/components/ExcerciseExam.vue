<script>
export default {
    props:['images'],
    created() {
        this.exam.total = this.images.length;
    },
    data() {
        return {
            started: false,
            examImages: [],
            exam: {
                current: 0,
                total: 0,
                showTitle: false,
            }
        }
    },
    methods: {
        initiateExam () {
            this.started = true;
            this.examImages = [...this.shuffle(this.images)];
        },
        shuffle(array) {
            let currentIndex = array.length,  randomIndex;

            // While there remain elements to shuffle.
            while (currentIndex > 0) {

                // Pick a remaining element.
                randomIndex = Math.floor(Math.random() * currentIndex);
                currentIndex--;

                // And swap it with the current element.
                [array[currentIndex], array[randomIndex]] = [
                array[randomIndex], array[currentIndex]];
            }

            return array;
        },
        nextImage(){
            this.exam.current ++;
            this.exam.showTitle = false;
        },
        restart () {
            this.examImages = [...this.shuffle(this.images)];
            this.exam.current = 0
            this.exam.showTitle = false;
        }
    },
}
</script>

<template>
    <div>
        <div class="text-center" v-show="!started">
            <button @click="initiateExam">START</button>
        </div>
        <div class="guess-image" v-if="started">
            <figure>
                <img :src="'/pato/images/Practice/'+examImages[exam.current].filename" :alt="examImages[exam.current].name" width="100%">
                <figcaption v-show="exam.showTitle">{{ examImages[exam.current].name }}</figcaption>
            </figure>

            <div class="navigation text-center">
                <button @click="exam.showTitle = true" v-show="!exam.showTitle">Покажи наименование</button>
                <button @click="nextImage" v-show="exam.current + 1 < exam.total">Следващо изображение</button>
                <button @click="restart" v-show="exam.current + 1 === exam.total">Рестартирай</button>
            </div>
        </div>
    </div>
</template>


<style scoped>
    .guess-image img{
        width: 100%;
        max-width: 720px;
        display: block;
        margin: 0 auto;
        border: 1px solid #ddd;
  padding: 10px;
    }
    .guess-image figure{
        text-align: center;
        font-size: 2rem;
        margin-bottom: 20px;
    }
</style>