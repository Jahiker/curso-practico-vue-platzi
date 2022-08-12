<template>
    <layout>
        <template #header>
            <Header />
        </template>
        <template #resume>
            <Resume :label="'Ahorro total'" :label-date="labelDate" :amount="amount" :total-amount="100000">
                <template #graphic>
                    <GraphicVue :amounts="amounts" />
                </template>
                <template #action>
                    <Action />
                </template>
            </Resume>
        </template>
        <template #movements>
            <Movements :movements="movements" />
        </template>
    </layout>
</template>

<script>
import Layout from "./Layout.vue";
import Header from "./Header.vue";
import Resume from "./Resume/Index.vue";
import Movements from "./Movements.vue";
import Action from "./Action.vue";
import GraphicVue from "./Graphic.vue";

export default {
    components: {
        Layout,
        Header,
        Resume,
        Movements,
        Action,
        GraphicVue
    },
    data() {
        return {
            amount: null,
            amounts: [100, 200, 500, 200, -400, -600, -300, 0, 300, 500],
            labelDate: null,
            movements: [{
                id: 0,
                title: "Movimiento 1",
                description: "Lorem ipsum dolor sit amet",
                amount: 1000,
            }, {
                id: 1,
                title: "Movimiento 2",
                description: "Lorem ipsum dolor sit amet",
                amount: -1000,
            }, {
                id: 2,
                title: "Movimiento 3",
                description: "Lorem ipsum dolor sit amet",
                amount: 1000,
            }, {
                id: 3,
                title: "Movimiento 4",
                description: "Lorem ipsum dolor sit amet",
                amount: 1000,
            }, {
                id: 4,
                title: "Movimiento 5",
                description: "Lorem ipsum dolor sit amet",
                amount: -1000,
            }, {
                id: 6,
                title: "Movimiento 7",
                description: "Lorem ipsum dolor sit amet",
                amount: -1000,
            }, {
                id: 7,
                title: "Movimiento 8",
                description: "Lorem ipsum dolor sit amet",
                amount: 1000,
            }, {
                id: 8,
                title: "Movimiento 9",
                description: "Lorem ipsum dolor sit amet",
                amount: 1000,
            }],
        }
    }
}
</script>