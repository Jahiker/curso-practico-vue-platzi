<template>
    <div :class="`movement ${ isNegative ? 'spend' : 'add' }`">
        <div class="content">
            <h4>{{ title }}</h4>
            <p>{{ description }}</p>
        </div>
        <div class="action">
            <img src="@/assets/trash-icon.svg" alt="Borrar" @click="remove">
            <p :class="{ 'red': isNegative, 'green': !isNegative }">{{ amountCurrency }}</p>
        </div>
    </div>
</template>

<script setup>
import { toRefs, computed } from 'vue';

const currencyFormater = new Intl.NumberFormat("es-US", {
    style: "currency",
    currency: "USD",
});

const amountCurrency = computed(() => {
    return currencyFormater.format(amount.value);
})

const isNegative = computed(() => amount.value < 0);


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
    }
});

const { id, title, description, amount } = toRefs(props);

const emit = defineEmits(["remove"]);

const remove = () => {
    emit("remove", id.value);
}

</script>

<style scoped>
.movement {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    padding: 16px;
    border-radius: 8px;
    box-sizing: border-box;
}

.movement.spend {
    background-color: #ffd8d8;
    border: 2px solid red;
}

.movement.add {
    background-color: #dcffd8;
    border: 2px solid green;
}

.movement .content {
    width: 100%;
}

.movement .action {
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    flex-direction: column;
}

h4,
p {
    margin: 0;
    padding: 0;
}

h4 {
    margin-bottom: 8px;
}

.movement .action img {
    margin-bottom: 16px;
}

.red {
    color: red;
    font-weight: bold;
}

.green {
    color: green;
    font-weight: bold;
}
</style>