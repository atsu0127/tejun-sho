<script setup lang="ts">
const cont = await queryContent("tejun").find();
const titles = cont
  .map((c) => c.title ?? "")
  .filter((t) => !t.includes("Vars"));
</script>

<template>
  <nav>
    <ul>
      <li v-for="(t, i) in titles" :key="i">
        <nuxt-link :to="`/tejun/${t}`">
          {{ t }}
        </nuxt-link>
      </li>
    </ul>
  </nav>
</template>
