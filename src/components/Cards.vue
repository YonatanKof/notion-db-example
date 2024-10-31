<script setup>
import { onMounted, ref } from 'vue';

const itemData = ref([]);

const getData = async () => {
	return fetch('/api/fetchNotion').then((res) => res.json());
};

onMounted(() => {
	getData().then((data) => {
		itemData.value = data.response.results;
	});
});
</script>

<template>
	<main>
		<article v-for="item in itemData">
			<h1 class="title">{{ item.properties.Name.title[0].plain_text }}</h1>
			<img :src="item.properties.Image.files[0].file.url" :alt="`Image of ${item.properties.Name.title[0].plain_text}`" />
		</article>
	</main>
</template>
