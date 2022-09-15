<template>
  <span @click="$emit('removePost', index)">{{ post }}</span>
</template>

<script>
export default {
  props: ['post', 'index']
}
</script>
