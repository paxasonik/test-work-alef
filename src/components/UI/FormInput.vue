<script setup>
import {Emit} from "@/utils/constants";
import {vMaska} from 'maska';

const props = defineProps({
	modelValue: [String, Number],
	type: {
		type: String,
		default: 'text'
	},
	name: String,
	label: String,
	id: String,
	placeholder: String,
	dataMaska: String,
	dataMaskaTokens: String,
});
const emit = defineEmits([
	Emit.UPDATE_VALUE
]);
const updateInput = (event) => {
	emit(Emit.UPDATE_VALUE, event.target.value)
}


</script>

<template>
	<div class="form__input">
		<label :for="props.id">{{ props.label }}</label>
		<input
			:type="props.type"
			:name="props.name"
			:placeholder="props.placeholder"
			:value="props.modelValue"
			:id="props.id"
			@input="updateInput"
			v-maska
			:data-maska="props.dataMaska"
			:data-maska-tokens="props.dataMaskaTokens"
		>
	</div>
</template>

<style scoped>

</style>