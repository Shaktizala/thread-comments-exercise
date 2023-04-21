<template>
  <span>{{ comment }}</span>

  <ul v-if="replies.length">
    <li>
      <div v-for="(item, index) in replies" :key="index">
        <Comment
          v-bind="{
            comment: item.comment,
            replies: item.comments,
          }"
        />
      </div>
    </li>
  </ul>
</template>

<script setup>
import { defineProps } from 'vue'

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
</script>
