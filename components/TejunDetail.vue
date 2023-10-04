<script setup lang="ts">
interface Props {
  tejunName: string;
}

const props = defineProps<Props>();

const { tejunName } = props;

const data = await queryContent("tejun")
  .where({ title: { $eq: tejunName } })
  .findOne();
const dataRef = ref(data);
const name = tejunName === "DB構築手順" ? "Construct" : "Remove";
const variablesData = await queryContent("tejun")
  .where({ title: { $eq: `${name}Vars` } })
  .findOne();
const variables = Object.entries(variablesData).filter(([k, v], i) => {
  console.log(k);
  return !k.startsWith("_") && k !== "title";
});
const variablesHolder = ref<any>({});
</script>

<template>
  <div v-for="([name, desc], i) in variables" :key="i">
    <label :for="name"> {{ name }}: </label>
    <input type="text" :name="name" v-model="variablesHolder[name]" />
    ({{ desc }})
  </div>
  <ContentRendererMarkdown :value="dataRef" :data="variablesHolder" />
</template>
