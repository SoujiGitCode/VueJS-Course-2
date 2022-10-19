<template>
  <div class="btn-group me-2 d-flex" role="group" aria-label="First group">
    <button type="button" class="btn btn-outline-primary"
            @click="customBefore" :disabled="firstPost=== 0">Prev {{firstPost}}</button>
    <button type="button" class="btn btn-outline-primary"
            @click="$emit('next')" :disabled="lastPost === dataLength">Next {{lastPost}}</button>
  </div>
</template>

<script setup>
const customBefore = () =>{
  emit ('before')

  console.log(dataLength)
}
const emit = defineEmits(["before", "next"])

defineProps({
  postByPage: Number,
  firstPost: Number,
  lastPost: Number,
  dataLength: Number
})
</script>

<style scoped>

</style>