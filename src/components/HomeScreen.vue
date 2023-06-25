<script setup>
    import { ref } from 'vue';
    import LayoutComponent from './LayoutComponent.vue';
    import HeaderComponent from './HeaderComponent.vue';
    import MovementsScreen from './MovementsScreen.vue';
    import ResumeIndex from './Resume/ResumeIndex.vue';
    const label = ref(null);
    const amount = ref(null);
    const options = {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric',
    };
</script>

<template>
    <LayoutComponent>
        <template #header>
            <HeaderComponent />
        </template>
        <template #resume>
            <ResumeIndex
                :label="label"
                :date-label="new Date(Date.now()).toLocaleDateString('es-CO', options)"
                :total-amount="1000000"
                :amount="amount"
            >
                <template #graphic> graphic </template>
                <template #action> action </template>
            </ResumeIndex>
        </template>
        <template #movements>
            <MovementsScreen />
        </template>
    </LayoutComponent>
</template>