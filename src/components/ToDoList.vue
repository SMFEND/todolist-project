<template lang="">
    <div>
        <ul>
            <ToDoItem 
            v-for="(todo, i) of todos" 
            v-bind:todo="todo" 
            v-bind:index="i"
            v-on:removeTodo="removeTodo"
            />
        </ul>  
    </div>
</template>
<script>

import ToDoItem from '@/components/ToDoItem'

export default {
    props: ['todos'],
    components: {
        ToDoItem,
    },

    methods: {
        removeTodo(id) {
            this.$emit('removeTodo', id)
        }
    },

}
</script>
<style lang="scss" scoped>
    ul {
        list-style-type: none;
        margin: 0;
        padding: 0;
    }
</style>