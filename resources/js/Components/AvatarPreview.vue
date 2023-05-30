<script setup lang="ts">
import { onMounted, ref } from "vue";

defineProps<{
    modelValue: string;
}>();

defineEmits(["update:modelValue"]);



const input = ref<HTMLInputElement | null>(null);

onMounted(() => {
    if (input.value?.hasAttribute("autofocus")) {
        input.value?.focus();
    }
});

const pickImage = (e) => {
    e.preventDefault();
    form.image = e.target.files[0];
    imagePreview = URL.createObjectURL(form.image);
};

defineExpose({ focus: () => input.value?.focus() });
</script>

<template>
    <img
        v-if="modelValue"
        :src="modelValue"
        class="mx-auto mb-4 w-32 rounded-lg"
        alt="Avatar"
    />
    <img
        v-else
        src="https://placekitten.com/250/250"
        class="mx-auto mb-4 w-32 rounded-lg"
        @click="$refs.file.click()"
        alt="Avatar"
    />

    <h5 class="mb-2 text-xl font-medium leading-tight">
        Click Image to Select Your Avatar
    </h5>

    <input
        class="border-gray-300 dark:border-gray-700 dark:bg-gray-900 dark:text-gray-300 focus:border-indigo-500 dark:focus:border-indigo-600 focus:ring-indigo-500 dark:focus:ring-indigo-600 rounded-md shadow-sm"
        :value="modelValue"
        @input="
            $emit(
                'update:modelValue',
                ($event.target as HTMLInputElement).value
            )
        "
        ref="input"
    />
</template>
