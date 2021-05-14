<template>
    <form @submit.prevent="OnSubmit">
        <input type="text" v-model="content">
        <button type="submit">Add ToDo</button>
    </form>
</template>

<script>
    export default {

        data() {
            return {
                content: ''
            }
        },   
        
        methods: {
            OnSubmit() {
                 if (this.content.trim()) {
                     const newTodo = {
                         id: Date.now(),
                         title: this.content,
                         completed: false
                     }

                    this.$emit('new-todo', newTodo)
                    this.content = ''
                 }
            }
    }
}


</script>

<style lang="scss" scoped>
    form {
        display: flex;
        justify-content: center;
    }
    input {
        width: 400px;
    }
</style>