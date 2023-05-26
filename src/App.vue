<script setup>
import {RouterView} from 'vue-router'
</script>

<template>
	<header class="header">
		<RouterLink :to="{name : 'home'}" class="header__login">
			<img src="@/assets/logo.svg">
		</RouterLink>
		<div class="header__nav nav">
			<RouterLink :to="{name : 'form'}" class="nav__link">
				Форма
			</RouterLink>
			<RouterLink :to="{name : 'home'}" class="nav__link">
				Превью
			</RouterLink>
		</div>
	</header>

	<main class="content">
		<RouterView/>
	</main>

	<footer class="footer">
		all rights reserved
	</footer>
</template>
