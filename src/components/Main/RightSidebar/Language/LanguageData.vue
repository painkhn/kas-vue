<script setup lang="ts">
import type { PrimitiveProps } from 'radix-vue';
import type { HTMLAttributes } from 'vue'

import Collapsible from '@/components/ui/collapsible/Collapsible.vue';
import SidebarGroup from '@/components/ui/sidebar/SidebarGroup.vue';
import SidebarMenu from '@/components/ui/sidebar/SidebarMenu.vue';
import SidebarMenuButton from '@/components/ui/sidebar/SidebarMenuButton.vue';
import SidebarMenuItem from '@/components/ui/sidebar/SidebarMenuItem.vue';
import { cn } from '@/lib/utils';
import { Dices } from 'lucide-vue-next';

const props = defineProps<PrimitiveProps & {
    class?: HTMLAttributes['class']
}>()

const data = {
    navMain: [
        {
            title: 'Russian',
            desription: 'Lorem ipsum',
            url: '#',
            icon: Dices,
            isActive: true,
        },
        {
            title: 'Espanol',
            desription: 'Lorem ipsum',
            url: '#',
            icon: Dices,
            isActive: true,
        },
        {
            title: 'Русский',
            desription: 'Lorem ipsum',
            url: '#',
            icon: Dices,
            isActive: true,
        },
    ],
}
</script>

<template>
    <SidebarGroup>
        <SidebarMenu class="gap-0 space-y-4">
            <Collapsible as-child class="group/collapsible">

            </Collapsible>
            <SidebarMenuItem v-for="item in data.navMain" :key="item.title" :default-open="item.isActive"
                :tooltip="item.title">
                <SidebarMenuButton class="px-2 py-0 h-auto" :class="cn(
                    'duration-100',
                    'group-data-[collapsible=icon]:p-0',
                    props.class)">
                    <span class="text-base">{{ item.title }}</span>
                </SidebarMenuButton>
            </SidebarMenuItem>
        </SidebarMenu>
    </SidebarGroup>
</template>