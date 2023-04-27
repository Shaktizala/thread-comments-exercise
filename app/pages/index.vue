<script setup>
let message = ref('')
let arraycomment = ref()

let { data: comments, pending } = useLazyAsyncData('place', () =>
  $fetch('http://localhost:5000/comments')
)
arraycomment.value = comments.value
function addToArray() {
  const arrObj = {
    _id: '',
    picture: '',
    auther: '',
    gender: '',
    comment: message.value,
    liked: true,
    isActive: true,
  }
  arraycomment.value.push(arrObj)
  message.value = ''
}
</script>
<template>
  <div class="ms-5">
    <div class="d-block">
      <input v-model="message" type="text" name="comment" class="m-3" />
      <button class="btn btn-primary" @click="addToArray()">Add</button>
    </div>
    <div v-for="(item, index) in comments" :key="index">
      <Comment
        v-bind="{
          comment: item.comment,
          replies: item.comments,
        }"
      />
    </div>
  </div>
</template>
<style scoped></style>
