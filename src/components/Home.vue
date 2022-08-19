<template>
    <layout>
        <template #header>
            <Header />
        </template>
        <template #resume>
            <Resume 
            :label="'Ahorro total'" 
            :label-date="labelDate" 
            :total-amount="100000"
            :amount="amount" 
            >
                <template #graphic>
                    <GraphicVue :amounts="amounts" />
                </template>
                <template #action>
                    <Action @create="create" />
                </template>
            </Resume>
        </template>
        <template #movements>
            <Movements :movements="movements" @remove="remove" />
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
            labelDate: null,
            movements: [{
                id: 0,
                title: "Movimiento 1",
                description: "Lorem ipsum dolor sit amet",
                amount: 100,
                time: new Date("08-01-2022")
            }, {
                id: 1,
                title: "Movimiento 2",
                description: "Lorem ipsum dolor sit amet",
                amount: 200,
                time: new Date("08-01-2022")
            }, {
                id: 2,
                title: "Movimiento 3",
                description: "Lorem ipsum dolor sit amet",
                amount: 500,
                time: new Date("08-01-2022")
            }, {
                id: 3,
                title: "Movimiento 4",
                description: "Lorem ipsum dolor sit amet",
                amount: 200,
                time: new Date("08-01-2022")
            }, {
                id: 4,
                title: "Movimiento 5",
                description: "Lorem ipsum dolor sit amet",
                amount: -400,
                time: new Date("08-01-2022")
            }, {
                id: 5,
                title: "Movimiento 7",
                description: "Lorem ipsum dolor sit amet",
                amount: -600,
                time: new Date("08-01-2022")
            }, {
                id: 6,
                title: "Movimiento 8",
                description: "Lorem ipsum dolor sit amet",
                amount: -300,
                time: new Date("08-01-2022")
            }, {
                id: 7,
                title: "Movimiento 9",
                description: "Lorem ipsum dolor sit amet",
                amount: 0,
                time: new Date("08-01-2022")
            }, {
                id: 8,
                title: "Movimiento 10",
                description: "Lorem ipsum dolor sit amet",
                amount: 300,
                time: new Date("07-01-2022")
            }, {
                id: 9,
                title: "Movimiento 11",
                description: "Lorem ipsum dolor sit amet",
                amount: 500,
                time: new Date("07-01-2022")
            }],
        }
    },
    computed: {
        amounts() {
            const lastDays = this.movements.filter(m => {
                const today = new Date();
                const oldDate = today.setDate(today.getDate() - 30);

                return m.time > oldDate;
            }).map(m => m.amount)

            return lastDays.map((m, i) => {
                const lastMovements = lastDays.slice(0, i);

                return lastMovements.reduce((suma, movement) => {
                    return suma + movement;
                }, 0)
            })
        }
    },
    methods: {
        create(movement) {
            this.movements.push(movement);
        },
        remove(id) {
            this.movements = this.movements.filter(m => m.id != id);
        }
    }
}
</script>