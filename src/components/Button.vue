<template>
    <button @click="onClick()" class="btn" :style="{ background: color }">{{ text }}</button>
</template>

<script>
export default {
    name: 'App-Button',
    props: {
        text: String,
        color: String
    },
    methods: {
        onClick() {
            this.$emit('btn-click')
        }
    }
}
</script>