<template>
    <div class="movement">
        <div class="content">
            <h4>{{ title }}</h4>
            <p>{{ description }}</p>
        </div>
        <div class="action">
            <img src="../../assets/trash-icon.svg" alt="Borrar" @click="remove" />
            <p :class="{ red: isNegative, green: !isNegative }">{{ amountToCurrency }}</p>
        </div>
    </div>
</template>

<script setup>
    import { computed, toRefs } from 'vue';

    const currencyFormatter = new Intl.NumberFormat('es-CO', {
        style: 'currency',
        currency: 'COP',
    });

    const props = defineProps({
        id: {
            type: Number,
        },
        title: {
            type: String,
        },
        description: {
            type: String,
        },
        amount: {
            type: Number,
        },
    });

    const { id, title, description, amount } = toRefs(props);

    const amountToCurrency = computed(() => currencyFormatter.format(amount.value));

    const isNegative = computed(() => amount.value < 0);

    const emit = defineEmits(['remove']);

    const remove = () => emit('remove', id.value);
</script>

<style scoped lang="scss">
    .movement {
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 100%;
        padding: 16px;
        background-color: #e6f9ff;
        border-radius: 8px;
        box-sizing: border-box;
        .content {
            width: 100%;
        }
        .action {
            display: flex;
            justify-content: space-between;
            align-items: flex-end;
            flex-direction: column;
            img {
                margin-bottom: 16px;
            }
        }
    }
    h4,
    p {
        margin: 0;
        padding: 0;
    }
    h4 {
        margin-bottom: 8px;
    }
    .red {
        color: red;
    }
    .green {
        color: green;
    }
</style>
