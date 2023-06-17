<script setup>
    import { ref } from 'vue';

    const showMovements = ref(false);
</script>

<template>
    <div class="header">
        <slot name="header"></slot>
    </div>
    <div class="resume">
        <slot name="resume"></slot>
    </div>
    <div class="movements">
        <div class="head" @click="showMovements = !showMovements">
            <div class="grip"></div>
        </div>
        <div class="body" v-show="showMovements">
            <slot name="movements"></slot>
        </div>
    </div>
</template>

<style lang="scss" scoped>
    .header,
    .resume,
    .movements {
        box-sizing: border-box;
        padding: 14px 0;
        display: flex;
        justify-content: space-around;
        align-items: center;
    }
    .header {
        position: fixed;
        width: 100vw;
    }
    .resume {
        min-height: 100vh;
    }
    .movements {
        position: absolute;
        bottom: 0;
        z-index: 1;
        width: 100vw;
        flex-direction: column;
        border-radius: 24px;
        background-color: white;
        box-shadow: 0 -8px 16px #e5e5e5;
        .head {
            box-sizing: border-box;
            width: 100%;
            padding: 24px;
            display: flex;
            justify-content: center;
            align-items: center;
            .grip {
                width: 120px;
                height: 8px;
                border-radius: 4px;
                background-color: #e5e5e5;
            }
        }
        .body {
            width: 100%;
            height: 75vh;
        }
    }
</style>
