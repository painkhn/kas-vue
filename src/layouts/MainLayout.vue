<script setup lang=ts>
import Header from '@/components/Main/Header.vue';

import {
    SidebarInset,
    SidebarProvider,
} from '@/components/ui/sidebar'

import MainSidebar from '@/components/Main/MainSidebar/Index.vue';
import UserSidebar from '@/components/Main/RightSidebar/UserSidebar.vue';
import RightSidebarProvider from '@/components/Main/RightSidebar/RightSidebarProvider.vue';
import SidebarRightTrigger from '@/components/Main/RightSidebar/SidebarRightTrigger.vue';
import { Bell, Globe, User } from 'lucide-vue-next';
import { ref } from 'vue';
import Footer from '@/components/Main/Footer.vue';

// Состояние для отслеживания активного сайдбара
const activeSidebar = ref<'profile' | 'notifications' | 'language'>('profile');

// Функции для переключения состояния
const showProfile = () => {
    activeSidebar.value = 'profile';
};

const showNotifications = () => {
    activeSidebar.value = 'notifications';
};

const showLanguage = () => {
    activeSidebar.value = 'language';
};

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
    <SidebarProvider class="bg-[#0C202E] relative">

        <MainSidebar />

        <RightSidebarProvider class="bg-[#0C202E] relative">
            <SidebarInset class="bg-[#061724]">

                <Header>
                    <div class="flex items-center gap-4">
                        <SidebarRightTrigger v-if="user" @click="showProfile">
                            <User class="!w-6 !h-6" :class="activeSidebar === 'profile' ? 'text-blue-500' : ''" />
                        </SidebarRightTrigger>
                        <SidebarRightTrigger v-if="user" @click="showNotifications">
                            <Bell class="!w-6 !h-6" :class="activeSidebar === 'notifications' ? 'text-blue-500' : ''" />
                        </SidebarRightTrigger>
                        <SidebarRightTrigger v-if="user" @click="showLanguage">
                            <Globe class="!w-6 !h-6" :class="activeSidebar === 'language' ? 'text-blue-500' : ''" />
                        </SidebarRightTrigger>
                    </div>
                </Header>
                <div>
                    <slot />
                </div>
                <Footer />
            </SidebarInset>
            <UserSidebar v-if="user" :active-sidebar="activeSidebar" />
        </RightSidebarProvider>

    </SidebarProvider>


</template>