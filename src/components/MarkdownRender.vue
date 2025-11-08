<!-- MarkdownRenderer.vue -->
<template>
  <div class="markdown-body" v-html="sanitizedHtml"></div>
</template>

<script setup lang="ts">
import { computed } from "vue";
import DOMPurify from "dompurify";
import { marked } from "marked";

const props = defineProps(["content"]);

// 配置 marked 选项
marked.setOptions({
  gfm: true,
  breaks: true,
});

const sanitizedHtml = computed(() => {
  if (!props.content) return "";

  const html = marked.parse(props.content);
  return DOMPurify.sanitize(html as string, {
    FORBID_TAGS: ["style", "script", "iframe"],
    FORBID_ATTR: ["onerror", "onclick", "onload"],
  });
});
</script>

<style scoped>
/* 这里可以复用您原来的样式 */
.markdown-body {
  line-height: 1.6;
  font-size: 18px;
}

.markdown-body :deep(h1) {
  font-size: 1.6em;
  margin: 1em 0;
}
</style>
