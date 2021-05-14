<template>
    <li>
        <span v-bind:class="{done: todo.completed}">
            <input type="checkbox" v-on:change="todo.completed = !todo.completed" v-bind:checked="todo.completed">
            <strong>
                {{this.index + 1 + ")"}} 
                {{todo.title | uppercase}}
                </strong>
        </span>
        <button v-on:click="$emit('removeTodo', todo.id)">&times;</button>
    </li>
</template>

<script>
    export default {
        props: {
            todo: {
                type: Object, 
                required: true
            },
            index: Number
        },

        filters: {
            uppercase(value) {
                 return value.toUpperCase();
            }
        }
}
</script>

<style lang="scss" scoped>
    li {
        display: flex;
        border: 1px solid black;
        justify-content: space-between;
        padding: .5rem 2rem;
        margin: .5rem 2rem;

        & strong {
            margin-left: 10px;
        }

        & button {
            border-radius: 25%;
            color: white;
            background-color: rgb(10, 36, 36);
            border: 3px solid white;
        }
    }

    .done {
        text-decoration: line-through;
    }

</style>