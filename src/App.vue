<template>
  <div id="app">
    <header>
      <h1>TodoList</h1>
      <input type="text" class="todo-input" placeholder="你想干点啥" @keydown.enter="addTodo" v-model="todoContent">
    </header>
    <section class="main">
      <ul class="todo-list">
        <li class="todo-item"
            v-for="(item, index) in todoList" :key="index"
            :class="{completed: item.complete}"
        >
          <span class="item-content">{{item.content}}</span>
          <input type="text" class="edit-content" :ref="item.id"
                 @blur="comfirmEdit(item)"
                 @keydown.enter="comfirmEdit(item)"
                 @keydown.esc="cancelEdit($event,item)"
                 v-model="item.content"
          >
          <div class="actions">
            <i class="check"
               @click="completeTodo(item)"
               :class="[item.complete? 'el-icon-refresh' : 'el-icon-circle-check-outline']"
            ></i>
            <i class="el-icon-edit edit" @click="editTodo($event,item)"></i>
            <i class="el-icon-delete delete" @click="removeTodo(item)"></i>
          </div>
        </li>
      </ul>
    </section>
  </div>
</template>

<script>

const STORAGE_KEY = 'my-todo'

const todoStorage = {
  save(todoList){
    localStorage.setItem(STORAGE_KEY, JSON.stringify(todoList))
  },
  get(){
    return JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]')
  }
}

export default {
  name: 'app',
  data(){
    return {
      completed: false,
      todoList: [],
      todoContent: '',
      editingTodo: ''
    }
  },
  components: {

  },
  methods: {
    editTodo(e,item){
      let input = this.$refs[item.id][0]
      input.classList.add('editing')
      input.focus()
      this.editingTodo = item
      this.beforeEditCache = item.content
    },
    comfirmEdit(item){
      let input = this.$refs[item.id][0]
      input.classList.remove('editing')
      if(!this.editingTodo) return
      this.editingTodo = null
      if(!item.content.trim()){
        this.removeTodo(item)
      }
    },
    addTodo(e){
      let value = this.todoContent && this.todoContent.trim()
      if(!value) return
      if(value){
        this.todoList.unshift({
          id: Math.round(Math.random()*100000),
          content: value,
          complete: false
        })
      }
      e.currentTarget.blur()
      this.todoContent = ''
      todoStorage.save(this.todoList)
    },
    cancelEdit(e,item){
      this.editingTodo = null
      item.content = this.beforeEditCache
      e.currentTarget.blur()
    },
    removeTodo(todo){
      let index = this.todoList.findIndex( item => {
        return item.id === todo.id
      })
      this.todoList.splice(index,1)
    },
    completeTodo(item){
      item.complete = !item.complete
    }
  },
  created(){
    this.todoList = todoStorage.get()
  },
  watch:{
    todoList: {
      handler(todos){
        todoStorage.save(todos)
      },
      deep: true
    }
  }
}
</script>

<style lang="scss">

  @mixin positionCenter {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  $edit-color: #4e90f2;
  $delete-color: #ff7573;
  $complete-color: #44e99a;

  #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  header {
    @include positionCenter;
    width: 100%;
    margin-top: 2%;
    display: flex;
    flex-direction: column;
    h1{
      margin-bottom: 20px;
      font-size: 40px;
      color: #ddd;
    }
    .todo-input {
      padding: 0 10px;
      height: 56px;
      width: 50%;
      outline: none;
      border: 1px solid #eee;
      background: #fbfbfb;
      border-radius: 4px;
      font-size: 16px;
      transition: all 0.3s;
      &::placeholder {
        color: #ccc
      }
      &:focus {
        background: #fff;
        border: 1px solid #ddd;
        box-shadow: 0 4px 8px -4px rgba(0,0,0,0.1),0 14px 16px -4px rgba(0,0,0,0.06);
      }
    }
  }
  section {
    @include positionCenter;
    width: 100%;
    ul{ width: 50%; margin-top: 16px;
      li{
        padding: 10px 0;
        line-height: 20px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        position: relative;
        border-bottom: 1px solid #f1f1f1;
        &:hover{
          .actions {
            visibility: visible;
          }
        }
        &.completed {
          .item-content { color: #999; text-decoration: line-through;}
        }
        .item-content { color: #333;}
        .edit-content {
          display: none;
          outline: none;
          border: none;
          height: 100%;
          width: calc( 100% - 96px );
          position: absolute;
          font-size: 14px;
          padding: 0 10px;
          &.editing {
            display: block;
          }
        }
        .actions {
          font-size: 16px;
          display: flex;
          visibility: hidden;
          i{
            @include positionCenter;
            height: 32px;
            width: 32px;
            border-radius: 50%;
            color: #999;
            &:hover{
              cursor: pointer;
            }
          }
          .edit:hover {
            color: $edit-color;
          }
          .check:hover {
            color: $complete-color;
          }
          .delete:hover {
            color: $delete-color;
          }
        }
      }
    }
  }
}
</style>
