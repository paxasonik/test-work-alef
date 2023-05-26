<script setup>
import {ref, watch} from "vue";
import {usePreviewStore} from "@/stores/preview";
import {useRouter} from "vue-router";
import FormInput from "@/components/UI/FormInput.vue";

const previewStore = usePreviewStore();
const router = useRouter();

const isChangedForm = ref(false);
const form = ref({
	name: '',
	age: '',
	children: [
		{
			name: '',
			age: '',
		}
	]
})

const addChildren = () => {
	form.value.children.push({
		name: '',
		age: '',
	});
}
const deleteChildren = (index) => {
	form.value.children.splice(index, 1);
}
const submit = () => {
	previewStore.previews.push(form.value);
	router.push({name: 'home'});
}

watch(() => form.value, (newVal, oldVal) => {
	isChangedForm.value = newVal.name !== '' && newVal.age !== ''
}, {deep: true});

</script>

<template>
	<section class="container">
		<form class="content__form form">
			<div class="form__parent">
				<h3 class="form__title">Персональные данные</h3>
				<FormInput
					type="text"
					v-model="form.name"
					label="Имя"
					id="parent_name"
					data-maska="X"
					data-maska-tokens="X:[а-яёА-ЯЁa-zA-Z\s-]:multiple"
				/>
				<FormInput
					type="text"
					v-model.number="form.age"
					label="Возраст"
					id="parent_age"
					data-maska="###"
				/>
			</div>
			<div class="form__children">
				<div class="form__row">
					<h3 class="form__title">Дети (макс. 5)</h3>
					<button class="button button__plus" @click.prevent="addChildren" v-if="form.children.length < 5">Добавить ребенка</button>
				</div>
				<ul class="form__list">
					<li class="form__item" v-for="(item, index) in form.children" :key="index">
						<FormInput
							type="text"
							v-model="item.name"
							label="Имя"
							:id="'children_name' + index"
							data-maska="X"
							data-maska-tokens="X:[а-яёА-ЯЁa-zA-Z\s-]:multiple"
						/>
						<FormInput
							type="text"
							v-model.number="item.age"
							label="Возраст"
							:id="'children_age' + index"
							data-maska="###"
						/>
						<button class="button button__not-border" @click.prevent="deleteChildren(index)">Удалить</button>
					</li>
				</ul>
			</div>
			<button class="button button__bg" type="submit" @click.prevent="submit" :disabled="!isChangedForm">Сохранить</button>
		</form>
	</section>
</template>