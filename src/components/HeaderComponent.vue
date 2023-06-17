<script setup>
    const reload = () => location.reload();
</script>

<template>
    <header>
        <img @click="reload" src="../assets/cashflow-icon.svg" alt="Logo" />
        <h1 @click="reload">Cash<span>Flow</span></h1>
        <span></span>
    </header>
</template>

<style lang="scss" scoped>
    header {
        display: flex;
        justify-content: space-around;
        align-items: center;
        width: 100vw;
        img,
        span {
            width: 48px;
        }
        h1 {
            font-size: 1.4rem;
            color: var(--brand-blue);
            span {
                color: var(--brand-green);
            }
        }
    }
</style>
