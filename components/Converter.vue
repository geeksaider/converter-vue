<script setup>
const selectedValue = ref("");
const fromConvert = ref("");
const inConvert = ref("");
const inputValue = ref("");
const resultConvert = ref("");

const nameConvertType = {
    mass: "Масса",
    valuta: "Валюта",
    distance: "Расстояние",
    speed: "Скорость",
};

const typesConvert = [
    { name: "Килограмм", value: "mass", weight: 1 },
    { name: "Грамм", value: "mass", weight: 0.001 },
    { name: "Тонна", value: "mass", weight: 1000 },
    { name: "Центнер", value: "mass", weight: 100 },
    { name: "Рубль", value: "valuta", weight: 0.01 },
    { name: "Доллар", value: "valuta", weight: 1 },
    { name: "Евро", value: "valuta", weight: 1.08 },
    { name: "Юань", value: "valuta", weight: 0.14 },
    { name: "Лира", value: "valuta", weight: 0.029 },
    { name: "Сантиметр", value: "distance", weight: 1 },
    { name: "Дециметр", value: "distance", weight: 10 },
    { name: "Метр", value: "distance", weight: 100 },
    { name: "Километр", value: "distance", weight: 100000 },
    { name: "Милиметр", value: "distance", weight: 0.1 },
    { name: "м/с", value: "speed", weight: 1 },
    { name: "м/ч", value: "speed", weight: 3600 },
    { name: "м/м", value: "speed", weight: 60 },
    { name: "км/ч", value: "speed", weight: 3.6 },
    { name: "км/с", value: "speed", weight: 0.001 },
    { name: "км/м", value: "speed", weight: 0.06 },
];

const oneFamilyType = ref([]);

watch(selectedValue, () => {
    oneFamilyType.value = typesConvert.filter(
        (v) => v.value == selectedValue.value
    );
});

function convertation() {
    let valueIn = "";
    let valueFrom = "";
    for (const convertValues of oneFamilyType.value) {
        if (convertValues.name == inConvert.value) {
            valueIn = convertValues.weight;
        }
        if (convertValues.name == fromConvert.value) {
            valueFrom = convertValues.weight;
        }
    }
    console.log(valueIn, valueFrom);
    resultConvert.value = (inputValue.value * valueFrom) / valueIn;
    resultConvert.value = Math.round(resultConvert.value * 1000) / 1000;
}
</script>

<template>
    <div
        class="flex flex-col items-center gap-8 w-[700px] bg-stone-100 p-28 rounded-3xl"
    >
        <h1 class="font-bold text-3xl">Конвертер</h1>
        <select
            class="bg-transparent text-stone-500 outline-none"
            name="quantities"
            id="quantities"
            v-model="selectedValue"
        >
            <option selected disabled value="">Тип велечины</option>
            <option value="mass">Вес, масса</option>
            <option value="valuta">Валюта</option>
            <option value="distance">Длинна, расстояние</option>
            <option value="speed">Скорость</option>
        </select>
        <div class="flex gap-7">
            <input
                class="bg-transparent outline-none text-stone-500"
                type="number"
                :placeholder="nameConvertType[selectedValue]"
                v-model="inputValue"
            />
            <span>из</span>
            <select
                class="bg-transparent outline-none text-stone-500"
                v-model="fromConvert"
            >
                <option v-for="quantities in oneFamilyType">
                    {{ quantities.name }}
                </option>
            </select>
            <span>в</span>
            <select
                class="bg-transparent outline-none text-stone-500"
                v-model="inConvert"
            >
                <option v-for="quantities in oneFamilyType">
                    {{ quantities.name }}
                </option>
            </select>
        </div>
        <button
            @click="convertation"
            class="bg-stone-400 px-6 py-4 rounded-full my-6 text-white hover:scale-125 transition-all"
        >
            Конвертировать
        </button>
        <span class="text-3xl text-stone-700 font-bold">
            {{ resultConvert }}
        </span>
    </div>
</template>
