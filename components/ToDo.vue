<script setup>
const valueToDo = ref("");
const todoList = ref([]);

function addToDo() {
    todoList.value.push(valueToDo.value);
    valueToDo.value = "";
}
function deleteToDo(todo) {
    todoList.value = todoList.value.filter((el) => {
        return el != todo;
    });
}
</script>

<template>
    <input placeholder="Введите что-нибудь" type="text" v-model="valueToDo" />
    <button @click="addToDo">Добавить</button>
    <div>
        <div v-for="todo in todoList">
            <span>{{ todo }}</span>
            <button @click="() => deleteToDo(todo)">Удалить</button>
        </div>
    </div>
</template>
