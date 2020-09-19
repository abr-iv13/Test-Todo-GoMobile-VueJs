<template>
    <div class="todo-list">
        <ul>
            <TodoItem 
                :key="todo.id"
                v-for="(todo, index) in todos"
                :index="index"
                :todo="todo"
                @remove-todo="removeTodo"
                @todo-data="todoData"
            />
        </ul>
    </div>
</template>

<style>
.todo-list {
    margin-top: 20px;
}
.todo-list > ul {
    list-style: none;
    margin: 0;
    padding: 0;
}
</style>

<script>
import TodoItem from './TodoItem'

export default {
    name: "TodoList",
    props: ['todos'],
    components: {
        TodoItem
    },
    methods: {
        removeTodo(id) {
            this.$emit("removeTodo", id)
        }, 
        todoData(todo) {
            this.$emit("todoData", todo)
        }
    }
}
</script>