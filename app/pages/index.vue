<script setup>
let message = ref('')
let isReply = ref(true)
let arraycomment = ref()

let { data: comments, pending } = useLazyAsyncData('place', () =>
  $fetch('http://localhost:5000/comments')
)
arraycomment.value = comments.value.comment
function addToArray() {
  arraycomment.value.push(message.value)
  message.value = ''
}
</script>
<template>
  <div class="d-block">
    <input v-model="message" type="text" name="comment" class="m-3" />
    <button class="btn btn-primary" @click="addToArray()">Add</button>
  </div>
  <ul v-for="(item, index) in comments" :key="index">
    <Comment
      v-bind="{
        comment: item.comment,
        replies: item.comments,
      }"
    />
  </ul>
</template>
<style scoped></style>
