<template>
    <div class="movement">
        <span>{{ title }}</span>
    </div>
</template>

<script setup>
import { defineProps, toRefs } from 'vue';

const props = defineProps({
    title: {
        type: String,
    }
});

const { title } = toRefs(props);

</script>