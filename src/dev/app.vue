<template>
    <div>
        <render ref="md" v-model="data"></render>
    </div>
</template>

<script>
import render from "../render.vue";
import content from "./assets/content_4";
export default {
    components: {
        render,
    },
    data() {
        return {
            data: content,
        };
    },
};
</script>

<style></style>
