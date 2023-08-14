<template>
    <form @submit.prevent="onSubmit">
        <label>Enter new task</label>
        <input type="text" v-model="inputTxt">
        <button type="submit">Create task</button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            inputTxt: ''
        }
    },
    methods:{
        onSubmit() {
            if(this.inputTxt.trim())
            {
                const newTask ={
                    id: Date.now(),
                    title: this.inputTxt,
                    completed: false
                }
                this.$emit('add-task', newTask);
                this.inputTxt='';
            }else{
                alert('Check your data! You can`t add empy task!');
            }
            
        }
    }
}
</script>
<style scoped>
    form{
        display: flex;
        justify-content: center;
        padding: 1rem;
    }
    input{
        width: 80%;
        margin: 1rem;
    }
    label{
        margin: 1rem;
    }
    button{
        background: linear-gradient(90deg, #e3f519, #f1a311);
    }
</style>