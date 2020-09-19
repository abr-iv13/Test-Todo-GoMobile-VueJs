<template>
  <div id="app">
    <div class="wrapper">
      <AddTodo @add-todo="addTodo"/>
      <hr>
      <!-- Сортировка -->

      <!-- <select v-model="search" >
        <option value="all" >Все</option>
        <option value="completed">Выполненые</option>
        <option value="active">Активные</option>
      </select> -->
      <div class="search">
        <input type="text" v-model="search" placeholder="Поиск">
        <div class="search__btn-group">
          <button>Все</button>
          <button>Активные</button>
          <button>Завершенные</button>
        </div>
      </div>
      
      <TodoList 
      :todos="filteredTodos"
      @removeTodo="removeTodo"
      @todoData="updateData"
      />
    </div>
  </div>
</template>
<style>

#app {
  display: flex;
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  overflow: auto;
}
.wrapper {
  background-color: rgb(0 0 0 / 10%);
  max-width: 500px;
  min-height: 500px;
  padding: 20px;
  border-radius: 10px ;
  right: 0;
  bottom: 0;
  left: 0;
  margin: auto;
  box-shadow: 0 1px 4px rgba(0, 0, 0, 1),
    -23px 0 20px -23px rgba(0, 0, 0, .8),
    23px 0 20px -23px rgba(0, 0, 0, .8),
    0 0 40px rgba(0, 0, 0, .1) inset;
}
.search {
  display: flex;
  justify-content: space-between;
}
.search > input {
  height: 22px;
  background-color: rgb(0 0 0 / 7%);
  border-radius: 5px;
  border: 1px solid black;
}
.search > input:hover {
  background:rgba(190, 190, 190, 0.863);
}
.search__btn-group > button {
  height: 25px;
  background-color: rgb(0 0 0 / 10%);
  border: 1px solid black;
  border-radius: 5px;
  margin-left: 10px;
}
.search__btn-group > button:hover {
  background:rgba(190, 190, 190, 0.863);
}

select {
  margin: 20px 0;
  font-size: 16px;
  width: 100%;
  height: 40px;
}

@media (max-width: 460px) {
  .search {
    flex-direction: column;
    align-items: center;
    margin-bottom: 10px;
  }
  .search__btn-group {
    margin-top: 12px;
  }
  .todo-list-item__btn {
    padding: 0;
  }
}
</style>

<script>
import TodoList from './components/TodoList'
import AddTodo from './components/AddTodo'

export default {
  name: "app",
  components: {
    TodoList,
    AddTodo
  },
  data() {
    return {
      todos:[
        {id: 1, name: "прочесть книгу", date: '19.7.2020', completed: false},
        {id: 2, name: "купить сыр", date: '19.7.2020', completed: false},
        {id: 3, name: "сделать уборку", date: '19.7.2020', completed: false}
      ],
      search: '',
    }
  },
  computed: {
    filteredTodos() {
      // Сортировка по полям
      // switch(this.search) {
      //   case 'all' : return this.todos;
      //   case 'completed' : return this.todos.filter(e => e.completed);
      //   case 'active' : return this.todos.filter(e => !e.completed);
      //   default : return this.todos
      // } 
       return this.todos.filter(todo => todo.name.indexOf(this.search.toLowerCase() ) !== -1)
    },
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(e => e.id !== id);
    },
    addTodo(newTodo) {
      this.todos.push(newTodo);
    },
    updateData(nameTodo) {
      let updateNameData = this.todos.find(item => item.id == nameTodo.id);
      updateNameData.name = nameTodo.name
    }
  },
  
}
</script>