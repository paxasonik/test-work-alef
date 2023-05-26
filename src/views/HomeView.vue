<script setup>
import {usePreviewStore} from "@/stores/preview";
import {DeclOfAge} from "@/utils/constants";
import {declOfNum} from "@/utils/helper";

const previewStore = usePreviewStore();
</script>

<template>
	<section class="container preview__list" v-if="previewStore.previews.length">
		<div class="preview__item" v-for="(item, index) in previewStore.previews">
			<div class="preview__parent parent">
				<h3 class="parent__title">{{ index + 1 }}. Персональные данные</h3>
				<div class="parent__data">
					{{ item.name }}, {{ item.age + declOfNum(item.age, DeclOfAge) }}
				</div>
			</div>
			<div class="preview__children children" v-if="item.children[0].name || item.children[0].age">
				<h3 class="children__title">Дети</h3>
				<ul class="children__list">
					<li class="children__item" v-for="(children, childrenIndex) in item.children" :key="childrenIndex">
						{{ children.name ? children.name : '' }}{{ children.name && children.age ? ', ' : '' }}
						{{ children.age ? children.age + declOfNum(children.age, DeclOfAge) : '' }}
					</li>
				</ul>
			</div>
		</div>
	</section>
	<section class="container content__preview preview" v-else>
		Добавьте персональные данные
		<RouterLink :to="{ name: 'form' }" class="button button__plus">
			Добавить
		</RouterLink>
	</section>
</template>