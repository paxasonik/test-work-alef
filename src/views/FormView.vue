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
	<section>
		<form class="">
			<div class="">
				<h3>Персональные данные</h3>
				<FormInput
					type="text"
					v-model="form.name"
					placeholder="Имя"
					data-maska="X"
					data-maska-tokens="X:[а-яёА-ЯЁa-zA-Z\s-]:multiple"
				/>
				<FormInput
					type="text"
					v-model.number="form.age"
					placeholder="Возраст"
					data-maska="###"
				/>
			</div>
			<div class="">
				<div class="">
					<h3>Дети (макс. 5)</h3>
					<button @click.prevent="addChildren" v-if="form.children.length < 5">Добавить ребенка</button>
				</div>
				<ul>
					<li v-for="(item, index) in form.children" :key="index">
						<FormInput
							type="text"
							v-model="item.name"
							placeholder="Имя"
							data-maska="X"
							data-maska-tokens="X:[а-яёА-ЯЁa-zA-Z\s-]:multiple"
						/>
						<FormInput
							type="text"
							v-model.number="item.age"
							placeholder="Возраст"
							data-maska="###"
						/>
						<button @click.prevent="deleteChildren(index)">Удалить</button>
					</li>
				</ul>
			</div>
			<button type="submit" @click.prevent="submit" :disabled="!isChangedForm">Сохранить</button>
		</form>
	</section>
</template>

<style scoped>

</style>