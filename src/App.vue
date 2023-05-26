<script setup>
import {RouterView} from 'vue-router'
</script>

<template>
	<header>
		<RouterLink :to="{name : 'home'}">
			<img src="@/assets/logo.svg">
		</RouterLink>
		<RouterLink :to="{name : 'form'}">
			Форма
		</RouterLink>
		<RouterLink :to="{name : 'home'}">
			Превью
		</RouterLink>
	</header>

	<main>
		<RouterView/>
	</main>

	<footer>
		all rights reserved
	</footer>
</template>

<style scoped>

</style>
