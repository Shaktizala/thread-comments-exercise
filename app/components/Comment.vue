<template>
  <div class="m-3">
    <p>{{ comment }}</p>
    <button @click="toggleInput()">reply</button>
    <div v-if="replies.length">
      <div class="ms-5">
        <div class="d-block" :class="!isReply ? 'd-none' : ''">
          <input v-model="message" type="text" name="comment" class="m-3" />
          <button class="btn btn-primary" @click="addToArray()">Add</button>
        </div>
        <div v-for="(item, index) in replies" :key="index">
          <Comment
            v-bind="{
              comment: item.comment,
              replies: item.comments,
            }"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'
let message = ref('')
let isReply = ref(false)
const props = defineProps({
  comment: {
    type: String,
    required: true,
  },
  replies: {
    type: Array,
    default: () => [],
  },
})

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
  console.log(props.replies)
  this.props.replies.push(arrObj)
  message.value = ''
}

function toggleInput() {
  isReply.value = !isReply.value
}
</script>
