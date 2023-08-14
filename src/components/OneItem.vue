<template>
    <li>
        <span :class="{finished: todo.completed}">
            <input type="checkbox"
            :checked="todo.completed"
            @change="checkboxChanged">
            <strong>{{index+1}}</strong>
            {{task.title}}
        </span>
        <span>
        <input type="text" v-model="newTitle" placeholder="Rename task here if u want!"/>
        <button @click="changeTitle">✏️</button>
        <button class="remove" 
        @click="$emit('remove-task', task.id)">X</button>
        </span>
    </li>
</template>

<script>
export default {
    data()
    {
        return {
            todo: this.task,
            newTitle:''
        }
    },
    props: {
        task: {
            type: Object,
            required: true
        },
        index: Number
    },
    methods:{
        checkboxChanged()
        {
            this.todo.completed = !this.todo.completed;
            this.$emit('checkbox-changed', this.todo);
        },
        changeTitle()
        {
            if(this.newTitle.trim())
            {
                this.todo.title=this.newTitle;
                this.$emit('name-changed', this.todo);
                this.newTitle='';
            }
            else {
                alert('Fill field please! U cannot rename to empty name!');
            }
            
        }
    }
}
</script>

<style scoped>
strong{
    margin-right: 2px;
}
    li{
        border: 3px double rgb(110, 1, 1);
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: .5rem 1rem;
        margin-right: 0.5rem;
        margin-bottom: 1rem;
        background-color: aliceblue;
    }
    span{
        display: flex;
        align-items: center;
    }
    .remove{
        margin-left: 10px;
        background-color: red;
        color: aqua;
        border-radius: 50%;
        cursor: pointer;
    }
    .finished
    {
        text-decoration: line-through;
        opacity: 0.5;
    }
</style>
