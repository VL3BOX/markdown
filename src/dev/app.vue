<template>
    <div>
        <mavon-render ref="md" v-model="data">
        </mavon-render>
    </div>
</template>

<script>
import mavonRender from '../mavon-render.vue'
import content from './assets/content_4'
export default {
    components: {
        mavonRender
    },
    data() {
        return {
            data: content
        }
    }
}
</script>

<style>

</style>