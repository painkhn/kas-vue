<script setup lang="ts">
import type { PrimitiveProps } from 'radix-vue';
import type { HTMLAttributes } from 'vue'
import Image from '@/components/Common/Image.vue';
import { ref } from 'vue';

import Button from '@/components/ui/button/Button.vue';
import Login from '@/components/Main/AuthModal/Login.vue';

import { cn } from '@/lib/utils'

import HeadData from './HeadData.vue';
import MiddleData from './MiddleData.vue'
import FooterData from './FooterData.vue';

import {
    Sidebar,
    SidebarContent,
    SidebarFooter,
    SidebarGroup,
    SidebarGroupLabel,
    SidebarHeader,
    SidebarRail,
    SidebarTrigger,
} from '@/components/ui/sidebar'

const props = defineProps<PrimitiveProps & {
    class?: HTMLAttributes['class']
}>()
const user = ref(null);

// Пример функции для аутентификации (замените на вашу логику)
const authenticateUser = async () => {
    // Здесь может быть запрос к API для аутентификации
    const response = await fetch('/api/auth/user');
    const data = await response.json();
    user.value = data.user;
};

// Вызов функции аутентификации при загрузке компонента
authenticateUser();
</script>

<template>
    <Sidebar collapsible="icon">
        <SidebarTrigger class="-right-5 top-[15%] absolute z-40 hover:bg-transparent w-7 h-7 transition-all">
            <Image :src="'/img/sidebarTrigger.svg'" class="shadow shadow-black rounded-full" />
        </SidebarTrigger>
        <SidebarHeader class="mb-5 shadow-md shadow-black/40">
            <div class="w-full py-3 flex justify-center items-center">
                <Image :src="'/img/sidebarHeader.svg'" />
            </div>
        </SidebarHeader>
        <SidebarContent class="px-4 space-y-4">
            <HeadData v-if="user" class="border-b border-black/40 px-0 py-4" />

            <MiddleData v-if="user" class="px-2" />

            <FooterData v-if="user" class="pt-4 border-t border-black/40" />

            <SidebarGroup v-else class="px-4">
                <div class="py-4 border-b border-[#1375E1] text-center space-y-4">
                    <SidebarGroupLabel class="px-0 text-lg inline text-center" :class="cn(
                        'duration-100',
                        'group-data-[collapsible=icon]:-mt-8 group-data-[collapsible=icon]:opacity-0',
                        props.class)">Авторизация</SidebarGroupLabel>
                    <h3 class="text-center" :class="cn(
                        'duration-100',
                        'group-data-[collapsible=icon]:-mt-8 group-data-[collapsible=icon]:opacity-0',
                        props.class)">Авторизируйтесь, чтобы начать играть прямо сейчас!</h3>
                    <Login>
                        <Button class="bg-[#1375E1] text-white hover:bg-blue-500" :class="cn(
                            'duration-100',
                            'group-data-[collapsible=icon]:-mt-8 group-data-[collapsible=icon]:opacity-0',
                            props.class)">Войти в аккаунт</Button>
                    </Login>
                </div>
            </SidebarGroup>
        </SidebarContent>
        <SidebarFooter>
            <!--  -->
        </SidebarFooter>
        <SidebarRail />
    </Sidebar>
    
</template>