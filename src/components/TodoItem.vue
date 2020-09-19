<template>
    <li>
       <div class="todo-list-item">
            <span :class="{done: todo.completed}">
                <input type="checkbox" @change="itemThrough">
                <p>{{index + 1}}</p>
            </span>
            <div :class="{done: todo.completed}" v-if="!editing"> {{todo.name | uppercase}} </div>
            <div v-else >
                <input 
                    type="text" 
                    placeholder="Введите название"
                    v-model="todo.name"
                > 
                <button class="btn_color btn" @click="editSave(todo)">ok</button>
                <button class="btn" @click="editCancel(todo)">x</button>
            </div>
            <div class="todo-list-item__btn">
                <span> {{todo.date}} </span>
                <button class="btn_color btn" @click="editEnter(todo)">r</button>
                <button class="btn" @click="$emit('remove-todo', todo.id)">&times;</button>
            </div>
       </div>
    </li>
</template>

<style scoped>
.todo-list-item__btn {
    display: flex;
    padding: 0 10px;
    align-items: center 
}
p {
    padding: 5px;
    margin: 0;
}
span {
    overflow: hidden;
    display: flex; 
    align-items: center;
    
}
.todo-list-item {
    font-size: 17px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 8px 2px;
    border: 1px solid black;
    border-radius: 10px;
    margin-bottom: 15px;
    box-shadow: 0 1px 2px rgba(0,0,0,0.25), 0 0 10px rgba(0,0,0,0.1) inset;
    transition: .2s linear;
}
.todo-list-item:hover {
    box-shadow: 0 0 5px 5px rgba(0,0,0,0.2);
}
.btn {
    text-align: center;
    background: rgb(233, 3, 3);
    border: 1px solid black;
    margin: 0 5px;
    border-radius: 5px;
    border-radius: 50%;
    width: 25px;
    height: 25px;
}
.btn_color {
    background: rgb(252, 124, 5);
}
.done {
    text-decoration: line-through;
}
@media (max-width: 460px) {
    .todo-list-item {
        padding: 0;
        font-size: 13px;
    }
    .todo-list-item__btn {
        padding: 0;
    }
}
</style>

<script>
export default {
    props: {
        todo: {
            type: Object
        },
        index: Number,
    },
    data() {
        return {
            editing: false,
            oldName: ''
        }
    },
    methods: {
        itemThrough() {
           this.todo.completed = !this.todo.completed
       },
        editEnter(todo) {
            this.oldName = todo.name;
            this.editing = true;
        },
        editCancel(todo) {
            todo.name = this.oldName;
            this.editing = false;
        },
        editSave(todo) {
            this.$emit('todo-data', todo)
            this.editing = false;
        }
        
    },
    filters: {
        uppercase(value) {
            return value.toUpperCase();
        }
    },
}
</script>