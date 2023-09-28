<script>
export default {
  props: ['excercises'],
}
</script>

<template>
    <ul>
        <li v-for="(excercise, key) in excercises" :key="'i'+key">
        <router-link :to="{name: 'excercise', params: {id: excercise.id}}">
          {{ excercise.title }} / {{ excercise.subtitle }}
        </router-link>
        </li>
    </ul>
</template>
