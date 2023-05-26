<script setup>
import {usePreviewStore} from "@/stores/preview";
import {DeclOfAge} from "@/utils/constants";
import {declOfNum} from "@/utils/helper";

const previewStore = usePreviewStore();
</script>

<template>
	<section v-if="previewStore.previews.length">
		<div class="" v-for="(item, index) in previewStore.previews">
			<div class="">
				<h3>{{ index + 1 }}. Персональные данные</h3>
				<div class="">
					{{ item.name }}, {{ item.age + declOfNum(item.age, DeclOfAge) }}
				</div>
			</div>
			<div class=""
					 v-if="item.children[0].name || item.children[0].age">
				<h3>Дети</h3>
				<ul>
					<li v-for="(children, childrenIndex) in item.children" :key="childrenIndex">
						{{ children.name ? children.name : '' }}{{ children.name && children.age ? ', ' : '' }}
						{{ children.age ? children.age + declOfNum(children.age, DeclOfAge) : '' }}
					</li>
				</ul>
			</div>
		</div>
	</section>
	<section v-else>
		<div class="">
			Добавьте персональные данные
			<RouterLink :to="{ name: 'form' }">
				Добавить
			</RouterLink>
		</div>
	</section>
</template>

<style scoped>

</style>