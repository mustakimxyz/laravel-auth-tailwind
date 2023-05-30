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

let image;
let imagePreview;

const pickImage = (e: any) => {
    console.log(e)
    e.preventDefault();
    image = e.target.files[0];
    imagePreview = URL.createObjectURL(image);
};

defineExpose({ focus: () => input.value?.focus() });
</script>

<template>
    <div class="text-center">
        <img
            v-if="imagePreview"
            :src="imagePreview"
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
            ref="file"
            type="file"
            name="upload"
            @input="pickImage"
            accept="image/png, image/gif, image/jpeg"
            hidden
            required
        />
    </div>
</template>
