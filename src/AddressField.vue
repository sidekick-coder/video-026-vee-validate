<script setup>
import { useField } from 'vee-validate';

const props = defineProps({
    name: {
        type: String,
        required: true
    }
})

const { value: state } = useField(`${props.name}.state`);
const { value: city } = useField(`${props.name}.city`);
const { value: address } = useField(`${props.name}.address`);
const { value: number } = useField(`${props.name}.number`);
</script>
<template>
  <div class="flex flex-col gap-y-2">
    <label class="flex justify-between">
        <span>state</span>
        <input class="w-[80%]" v-model="state" />
    </label>
    <label class="flex justify-between">
        <span>city</span>
        <input class="w-[80%]" v-model="city" />
    </label>
    <label class="flex justify-between">
        <span>address</span>
        <input class="w-[80%]" v-model="address" />
    </label>
    <label class="flex justify-between">
        <span>number</span>
        <input type="number" class="w-[80%]" v-model="number" />
    </label>
  </div>
</template>
