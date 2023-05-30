<script setup>
import GuestLayout from "@/Layouts/GuestLayout.vue";
import InputError from "@/Components/InputError.vue";
import InputLabel from "@/Components/InputLabel.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import TextInput from "@/Components/TextInput.vue";
import { Head, Link, useForm } from "@inertiajs/vue3";
import AvatarInput from "@/Components/AvatarInput.vue";

const form = useForm({
    name: "",
    image: "",
    imagePreview: "",
    email: "",
    password: "",
    password_confirmation: "",
});

const pickImage = (e) => {
    e.preventDefault();
    form.image = e.target.files[0];
    form.imagePreview = URL.createObjectURL(form.image);
};

const submit = () => {
    form.post(route("register"), {
        onFinish: () => form.reset("password", "password_confirmation"),
    });
};
</script>

<template>
    <GuestLayout>
        <Head title="Register" />

        <form @submit.prevent="submit" enctype="multipart/form-data">
            <div class="text-center">
                <img
                    v-if="form.imagePreview"
                    :src="form.imagePreview"
                    class="mx-auto mb-4 w-32 rounded-lg border-spacing-2"
                    alt="Avatar"
                />
                <img
                    v-else
                    :src="'../images/logo.png'"
                    class="mx-auto mb-4 w-32 rounded-lg border-spacing-2"
                    @click="$refs.file.click()"
                    alt="Avatar"
                />
                <InputLabel class="mb-2 text-xl font-medium leading-tight" value="Click Duck to Select Your Avatar"/>
                    
                <input
                    ref="file"
                    type="file"
                    @input="pickImage"
                    name="avatar"
                    accept="image/png, image/gif, image/jpeg"
                    hidden
                    required
                />
                <InputError class="mt-2" :message="form.errors.image" />
            </div>

            <div>
                <InputLabel for="name" value="Name" />

                <TextInput
                    id="name"
                    type="text"
                    class="mt-1 block w-full"
                    v-model="form.name"
                    required
                    autofocus
                    autocomplete="name"
                />

                <InputError class="mt-2" :message="form.errors.name" />
            </div>

            <div class="mt-4">
                <InputLabel for="email" value="Email" />

                <TextInput
                    id="email"
                    type="email"
                    class="mt-1 block w-full"
                    v-model="form.email"
                    required
                    autocomplete="username"
                />

                <InputError class="mt-2" :message="form.errors.email" />
            </div>

            <div class="mt-4">
                <InputLabel for="password" value="Password" />

                <TextInput
                    id="password"
                    type="password"
                    class="mt-1 block w-full"
                    v-model="form.password"
                    required
                    autocomplete="new-password"
                />

                <InputError class="mt-2" :message="form.errors.password" />
            </div>

            <div class="mt-4">
                <InputLabel
                    for="password_confirmation"
                    value="Confirm Password"
                />

                <TextInput
                    id="password_confirmation"
                    type="password"
                    class="mt-1 block w-full"
                    v-model="form.password_confirmation"
                    required
                    autocomplete="new-password"
                />

                <InputError
                    class="mt-2"
                    :message="form.errors.password_confirmation"
                />
            </div>

            <div class="flex items-center justify-end mt-4">
                
                <Link
                    :href="route('login')"
                    class="underline text-sm text-gray-600 dark:text-gray-400 hover:text-gray-900 dark:hover:text-gray-100 rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 dark:focus:ring-offset-gray-800"
                >
                    Already registered?
                </Link>
                <PrimaryButton
                    class="ml-4"
                    :class="{ 'opacity-25': form.processing }"
                    :disabled="form.processing"
                >
                    Register
                </PrimaryButton>
            </div>
        </form>
    </GuestLayout>
</template>
