<template>
  <MarkdownRender :content="content" />
</template>

<script setup>
import MarkdownRender from "./components/MarkdownRender.vue";
import { getPassage } from "./service/ApiPassage";
import { onMounted, ref } from "vue";

let content = ref("");

onMounted(async () => {
  let passage = await getPassage();
  content.value = passage;
});
</script>

<style scoped></style>
