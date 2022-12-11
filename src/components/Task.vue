<template>
    <div :key="i.id" v-for="i in task">
        <TaskRenderer @toggle-reminder="$emit('toggle-reminder', i.id)" @delete-task="$emit('delete-task', i.id)" :task="i"/>
    </div>
</template>

<script>
    import TaskRenderer from './TaskRenderer.vue'
    export default {
        name: 'App-Task',
        props: {
            task: Array
        },
        components: {
            TaskRenderer
        },
        emits: ['delete-task', 'toggle-reminder']
    }
</script>