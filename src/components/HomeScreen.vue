<script setup>
import {computed, ref} from 'vue';
    import LayoutComponent from './LayoutComponent.vue';
    import HeaderComponent from './HeaderComponent.vue';
    import MovementsScreen from './Movements/MovementsScreen.vue';
    import ResumeIndex from './Resume/ResumeIndex.vue';
    import ActionButton from './ActionButton.vue';
    import GraphicComponent from './Resume/GraphicComponent.vue';
    const label = ref(null);
    const amount = ref(null);
    const options = {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric',
    };
    const amounts = computed(() => {
        const lastDays = movements.filter(m => {
            const today = new Date();
            const oldDate = today.setDate(today.getDate() - 30);
            return m.time > oldDate;
        })
        .map(m => m.amount);
        return lastDays.map((m, i) => {
            const lastMovements = lastDays.slice(0, i);
            return lastMovements.reduce((summatory, movement) => summatory + movement, 0);
        })
    })
    const movements = [
        {
            id: 0,
            title: 'Movimiento #1',
            description: 'Una compra de gusto culposo',
            amount: 100000,
            time: new Date("07-15-2023"),
        },
        {
            id: 1,
            title: 'Movimiento #2',
            description: 'Una compra de gusto culposo',
            amount: 200000,
            time: new Date("07-15-2023"),
        },
        {
            id: 2,
            title: 'Movimiento #3',
            description: 'Una compra de gusto culposo',
            amount: -350000,
            time: new Date("07-15-2023"),
        },
        {
            id: 3,
            title: 'Movimiento #4',
            description: 'Una compra de gusto culposo',
            amount: 10000,
            time: new Date("07-15-2023"),
        },
        {
            id: 4,
            title: 'Movimiento #5',
            description: 'Una compra de gusto culposo',
            amount: -5000,
            time: new Date("07-15-2023"),
        },
        {
            id: 5,
            title: 'Movimiento #6',
            description: 'Una compra de gusto culposo',
            amount: 500000,
            time: new Date("07-15-2023"),
        },
        {
            id: 6,
            title: 'Movimiento #7',
            description: 'Una compra de gusto culposo',
            amount: 1400000,
            time: new Date("07-16-2023"),
        },
        {
            id: 7,
            title: 'Movimiento #8',
            description: 'Una compra de gusto culposo',
            amount: -16000,
            time: new Date("07-16-2023"),
        },
        {
            id: 8,
            title: 'Movimiento #9',
            description: 'Una compra de gusto culposo',
            amount: -850000,
            time: new Date("07-16-2023"),
        },
        {
            id: 9,
            title: 'Movimiento #10',
            description: 'Una compra de gusto culposo',
            amount: 99000,
            time: new Date("07-16-2023"),
        },
    ];
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
                <template #graphic>
                    <GraphicComponent :amounts="amounts" />
                </template>
                <template #action>
                    <ActionButton />
                </template>
            </ResumeIndex>
        </template>
        <template #movements>
            <MovementsScreen :movements="movements" />
        </template>
    </LayoutComponent>
</template>
