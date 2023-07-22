<script setup>
    import { computed, onMounted, ref } from 'vue';
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
        const lastDays = movements.value
            .filter((m) => {
                const today = new Date();
                const oldDate = today.setDate(today.getDate() - 30);
                return m?.time > oldDate;
            })
            .map((m) => m?.amount);
        return lastDays.map((m, i) => {
            const lastMovements = lastDays.slice(0, i + 1);
            return lastMovements.reduce((summary, movement) => summary + movement, 0);
        });
    });
    const movements = ref([]);
    const totalAmount = computed(() =>
        movements.value.reduce((summary, m) => summary + m?.amount, 0)
    );
    onMounted(() => {
        const savedMovements = JSON.parse(localStorage.getItem('movements'));
        if (Array.isArray(savedMovements)) {
            movements.value = savedMovements?.map((m) => ({ ...m, time: new Date(m?.time) }));
        }
    });
    const create = (movement) => {
        movements.value.push(movement);
        save();
    };
    const remove = (id) => {
        const index = movements.value.findIndex((m) => m?.id === id);
        movements.value.splice(index, 1);
        save();
    };
    const save = () => localStorage.setItem('movements', JSON.stringify(movements.value));
    const select = (el) => (amount.value = el);
</script>

<template>
    <LayoutComponent>
        <template #header>
            <HeaderComponent />
        </template>
        <template #resume>
            <ResumeIndex
                :amount="amount"
                :date-label="new Date(Date.now()).toLocaleDateString('es-CO', options)"
                :label="label"
                :total-amount="totalAmount"
            >
                <template #graphic>
                    <GraphicComponent :amounts="amounts" @select="select" />
                </template>
                <template #action>
                    <ActionButton @create="create" />
                </template>
            </ResumeIndex>
        </template>
        <template #movements>
            <MovementsScreen :movements="movements" @remove="remove" />
        </template>
    </LayoutComponent>
</template>