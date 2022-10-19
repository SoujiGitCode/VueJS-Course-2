<template>
<div class="card">
  <div class="card-body">
    <div class="card-tittle" :class="`text-${colorText}`">
      {{id}}{{title}}
    </div>
    {{body}}
  </div>

  <div class="col-2">
    <div class="row ">
        <button class="btn btn-outline-primary" @click="emit('markAsFav', title)" > Fav</button>
    </div>
  </div>

</div>
</template>

<script setup>
defineProps({
  title: String,
  colorText: {
    type: String,
    default: "primary"
  },
  id: Number,
  body:{
    type: String,
    default: "text body not defined"
  }
    }
)

const emit = defineEmits(["markAsFav"])


</script>

<style scoped>

</style>