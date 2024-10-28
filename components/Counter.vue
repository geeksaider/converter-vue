<script setup>
const count = ref(0);

function increment() {
    count.value++;
}

function decrement() {
    count.value--;
}
</script>

<template>
    <button @click="increment">Прибавить</button>
    <button @click="decrement">Убавить</button>
    <span>Кол-во: {{ count }}</span>
</template>
