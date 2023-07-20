<script setup>
    import { toRefs, computed } from 'vue';

    const props = defineProps({
        label: {
            type: String,
            defaul: Date.now().toLocaleString(),
        },
        dateLabel: String,
        totalAmount: Number,
        amount: {
            type: Number,
            defaul: null,
        },
    });

    const { label, dateLabel, totalAmount, amount } = toRefs(props);

    const visualAmount = computed(() => (amount.value !== null ? amount.value : totalAmount.value));
    const visualLabel = computed(() => (label.value !== null ? label.value : dateLabel.value));
    const currencyFormatter = new Intl.NumberFormat('es-CO', {
        style: 'currency',
        currency: 'COP',
    });
    const currencyAmount = computed(() => currencyFormatter.format(visualAmount.value));
</script>

<template>
    <main>
        <p>{{ visualLabel }}</p>
        <h1>{{ currencyAmount }}</h1>
        <div class="graphic">
            <slot name="graphic"></slot>
        </div>
        <div class="action">
            <slot name="action"></slot>
        </div>
    </main>
</template>

<style scoped lang="scss">
    main {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        width: 100%;
    }
    h1,
    p {
        margin: 0;
        text-align: center;
    }
    h1 {
        margin-top: 14px;
        color: var(--brand-green);
    }
    .graphic {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        padding: 48px 24px;
        box-sizing: border-box;
    }
</style>
