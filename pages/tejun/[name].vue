<script setup lang="ts">
import { useRoute } from "#app";

const route = useRoute();
const { name } = route.params;
</script>

<template>
  <TejunDetail :tejun-name="name as string"></TejunDetail>
</template>
