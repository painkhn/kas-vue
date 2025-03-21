<script setup lang="ts">
import Button from '@/components/ui/button/Button.vue';
import Input from '@/components/ui/input/Input.vue';
import Image from '@/components/Common/Image.vue';
import axios from 'axios';
import { ref } from 'vue'

import {
    Dialog,
    DialogContent,
    DialogDescription,
    DialogFooter,
    DialogHeader,
    DialogTitle,
    DialogTrigger,
} from '@/components/ui/dialog'

const form = ref({
    email: '',
    password: '',
    remember: false,
});

const errors = ref<Record<string, string>>({});

const submit = async () => {
    try {
        // Отправляем POST-запрос на сервер
        const response = await axios.post('/login', {
            email: form.value.email,
            password: form.value.password,
            remember: form.value.remember,
        });

        // Обработка успешного ответа
        if (response.data.success) {
            // Перенаправление или другие действия после успешного входа
            window.location.href = '/dashboard'; // Пример перенаправления
        }
    } catch (error: any) {
        // Обработка ошибок
        if (error.response && error.response.data.errors) {
            errors.value = error.response.data.errors; // Сохраняем ошибки
        } else {
            console.error('Ошибка при отправке формы:', error);
        }
    }
};
</script>

<template>
    <Dialog>
        <DialogTrigger>
            <slot />
        </DialogTrigger>
        <DialogContent class="bg-[#061724]">
            <DialogHeader class="space-y-2 mb-6">
                <DialogTitle class="text-center text-xl">Добро пожаловать!</DialogTitle>
                <DialogDescription class="text-center">
                    Нет аккаунта? <a href="#!" class="text-blue-600 underline">Зарегистрироваться</a>
                </DialogDescription>
            </DialogHeader>

            <form @submit.prevent="submit" class="space-y-4 grid grid-cols-1">
                <Input placeholder="Email" type="email" v-model="form.email"
                    class="shadow shadow-black border-0 bg-[#D6D6D6] text-black placeholder:text-black/80" required />
                <Input placeholder="Password" type="password" v-model="form.password"
                    class="shadow shadow-black border-0 bg-[#D6D6D6] text-black placeholder:text-black/80" required />
                <a class="text-blue-600 underline text-sm block ml-auto" href="#!">Забыли пароль?</a>
                <div class="py-3"></div>
                <Button type="submit" class="w-full bg-[#1375E1] text-white hover:bg-blue-500">Войти</Button>
                <div class="pt-6 space-y-6">
                    <div class="relative">
                        <div class="w-full border-b border-[#1375E1] absolute top-1/2"></div>
                        <p class="text-center relative z-40 max-w-[240px] mx-auto bg-[#061724]">или войти с помощью</p>
                    </div>
                    <div class="flex justify-around px-16">
                        <button>
                            <Image :src="'/img/facebook.svg'" />
                        </button>
                        <button>
                            <Image :src="'/img/google.svg'" />
                        </button>
                        <button>
                            <Image :src="'/img/twitch.svg'" />
                        </button>
                    </div>
                </div>
            </form>

            <DialogFooter>
                <!--  -->
            </DialogFooter>
        </DialogContent>
    </Dialog>
</template>