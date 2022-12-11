<template>
    <header>
        <h1>{{ title }}</h1>
        <Button @btn-click="$emit('show-add-task')" :text="AddTask ? 'Close' : 'Add Task'"
            :color="AddTask ? 'red' : 'green'"></Button>

    </header>
</template>

<script>
import Button from "./Button"
export default {
    name: 'App-Header',
    props: {
        'title': String,
        'AddTask': Boolean
    },
    emit: ['show-add-task'],
    components: {
        Button
    }
}
</script>

<style scoped>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>