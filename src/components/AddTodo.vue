<template>
    <form @submit.prevent="onSubmit">
        <input
         type="text" 
         placeholder="Введите задачу"
         v-model="name"
         >
        <button type="submit">Добавить</button>
    </form>
</template>

<style scoped>
form {
    margin: 15px 0px;
    display: flex;
    justify-content: space-between;
}
input {
    width: 100%;
    height: 25px;
    margin-right: 10px;
    border: 1px solid black;
    background-color: rgb(0 0 0 / 7%);
    border-radius: 10px;
}
input:hover {
    background:rgba(190, 190, 190, 0.863);
}
button {
    background-color:#e0e0e0b4;
    border: none;
    border: 1px solid black;
    border-radius: 10px;

}
button:hover {
    background:rgba(190, 190, 190, 0.863);
}
</style>

<script>
export default {
    data() {
        return {
            name: ''
        }
    },
    methods: {
        onSubmit() {
            if (this.name.trim()) {
               const newTodo = {
                   id: Date.now(),
                   name: this.name,
                   date: new Date().getDate() + '.' + new Date().getMonth() + '.' + new Date().getFullYear(),
                   completed: false
               }
               this.$emit('add-todo', newTodo)
               this.name = ''
            }
        }
    },
}
</script>