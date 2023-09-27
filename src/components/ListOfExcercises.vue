<script>
export default {
  props: ['excercises'],
}
</script>

<template>
    <ul>
        <li v-for="(excercise, key) in excercises" :key="'i'+key">
        {{ excercise.title }} / {{ excercise.subtitle }}

        </li>
    </ul>
</template>
