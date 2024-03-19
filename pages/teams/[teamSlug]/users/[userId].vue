<template>
  <p class="box">
    {{ message }}
  </p>
</template>

<script setup>
import { computed } from "vue";

const route = useRoute();

const message = computed(
  () => `I'm member of ${route.params.teamSlug}
    and my user id is ${route.params.userId}`
);
</script>
