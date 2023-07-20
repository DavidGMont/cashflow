<script setup>
    import { defineAsyncComponent } from 'vue';
    import SplashScreen from './components/SplashScreen.vue';

    const HomeScreen = defineAsyncComponent(() => {
        return new Promise((resolve) => {
            setTimeout(() => {
                resolve(import('./components/HomeScreen.vue'));
            }, 2500);
        });
    });
</script>

<template>
    <Transition name="bounce">
        <Suspense>
            <template #default>
                <HomeScreen />
            </template>
            <template #fallback>
                <SplashScreen />
            </template>
        </Suspense>
    </Transition>
</template>

<style>
    html,
    body,
    .app {
        margin: 0;
        font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif;
    }

    .app {
        min-height: 100vh;
    }

    :root {
        --brand-green: #04b500;
        --brand-blue: #0689b0;
    }

    .bounce-enter-from,
    .bounce-leave-to {
        opacity: 0;
    }

    .bounce-enter-active {
        animation: bounce-in 0.5s;
        transition: opacity 0.25s ease;
    }
    .bounce-leave-active {
        animation: bounce-in 0.5s reverse;
        transition: opacity 0.25s ease;
    }

    @keyframes bounce-in {
        0% {
            transform: scale(0);
        }
        50% {
            transform: scale(1.25);
        }
        100% {
            transform: scale(1);
        }
    }
</style>
