<template>
  <div class="nocodb">
    <input v-model="link" />
    {{ decodeLink }}
    <button @click="handleClick">Open in Nocodb</button>
  </div>
</template>

<script setup>
const link = ref("");
const decodeLink = computed(() => decodeURI(link.value));
function handleClick() {
  open("https://google.com");
}
</script>

