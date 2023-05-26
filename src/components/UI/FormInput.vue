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
	<input
		:type="props.type"
		:name="props.name"
		:placeholder="props.placeholder"
		:value="props.modelValue"
		@input="updateInput"
		v-maska
		:data-maska="props.dataMaska"
		:data-maska-tokens="props.dataMaskaTokens"
	>
</template>

<style scoped>

</style>