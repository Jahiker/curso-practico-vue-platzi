<template>
    <layout>
        <template #header>
            <Header />
        </template>
        <template #resume>
            <Resume 
            :label="'Ahorro total'" 
            :label-date="labelDate" 
            :total-amount="totalAmount"
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
            movements: [],
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
        },
        totalAmount() {
            return this.movements.reduce((suma, m) => {
                return suma + m.amount;
            }, 0)
        }
    },
    mounted() {
        const movements = JSON.parse(localStorage.getItem("movements"));

        if (Array.isArray(movements)) {
            this.movements = movements?.map(m => {
                return { ...m, time: new Date(m.time) }
            });
        }
    },
    methods: {
        create(movement) {
            this.movements.push(movement);
            this.save();
        },
        remove(id) {
            this.movements = this.movements.filter(m => m.id != id);
            this.save();
        },
        save() {
            localStorage.setItem("movements", JSON.stringify(this.movements));
        }
    }
}
</script>