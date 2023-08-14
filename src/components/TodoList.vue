<template>
<div>
    <ul>
        <OneItem v-for="(task, i) of tasks"
        :key="task.id"
        :task="task"
        :index="i"
        @remove-task="removeTask"
        @checkbox-changed="changingInput"
        @name-changed="nameChanged"/>
    </ul>
</div>
</template>

<script>
import OneItem from "@/components/OneItem";
export default {
    props: ['tasks'],
    components: {
        OneItem
    },
    methods:
    {
        removeTask(id)
        {
            this.$emit('remove-task', id);
        },
        changingInput(value)
        {
            this.$emit('checkbox-changed', value);
        },
        nameChanged(value){
            this.$emit('name-changed', value);
        }
    }
}
</script>

<style scoped>
    ul{
        list-style: none;
        margin: 0;
        padding: 0;
    }
</style>