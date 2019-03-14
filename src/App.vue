<template>
  <div id="app">
    <div class="wrapper">
      <header>Todos</header>
      <input type="text" class="todo" placeholder="输入清单">
      <section>
        <ul class="list">
          <li class="item">
            <el-checkbox v-model="completed" @change="xxx"></el-checkbox>
            <label>吃饭</label>
            <input type="text" class="todo-item">
          </li>
          <li class="item">
            <el-checkbox v-model="completed" @change="xxx"></el-checkbox>
            <label>吃饭</label>
            <input type="text" class="todo-item">
          </li>
          <li class="item">
            <el-checkbox v-model="completed" @change="xxx"></el-checkbox>
            <label>吃饭</label>
            <input type="text" class="todo-item">
          </li>
        </ul>
      </section>
    </div>
  </div>
</template>

<script>


export default {
  name: 'app',
  data(){
    return {
      completed: false
    }
  },
  components: {

  },
  methods: {
    xxx(){
      console.log('xxx')
    }
  }
}
</script>

<style lang="scss">

  $border-color: #ddd;
  $checked-bg: #eee;
  #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  .wrapper{
    width: 400px;
    box-shadow: 0 0 4px rgba(0,0,0,0.2);
    margin: 40px auto;
    header {
      height: 48px;
      width: 400px;
      line-height: 48px;
      font-weight: 800;
      font-size: 24px;
      padding-left: 16px;
      padding-top: 4px;
    }
    input{
      &.todo{
        height: 40px;
        width: 400px;
        border: none;
        outline: none;
        padding: 8px 16px 0 16px;
        border-bottom: 1px solid $border-color;
        &::placeholder {
          color: #ccc;
        }
      }
    }
    section{
      ul {
        margin-top: -1px;
        li {
          height: 44px;
          width: 100%;
          line-height: 44px;
          border-top: 1px solid $border-color;
          padding: 0 16px;
          .el-checkbox + label {
            position: absolute;
            padding: 0 10px;
            width: 320px;
          }
          input[type="text"] {
            height: 42px;
            border: none;
            margin-top: -1px;
            padding: 0 10px;
            width: 320px ;
            font-size: inherit;
            position: relative;
            display: none;
            outline: none;
          }
          label[for="todo"]{
            position: absolute;
            padding-left: 10px;
          }
        }
      }
    }
  }

}
</style>
