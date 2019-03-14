<template>
  <div id="app">
    <div class="wrapper">
      <header>Todos</header>
      <input type="text" class="todo" placeholder="输入清单">
      <section>
        <ul class="list">
          <li class="item">
            <input id="toggle" type="checkbox" style="display: none">
            <label for="toggle"></label>
            <label for="todo">吃饭</label>
            <input type="text" id="todo">
          </li>
          <li class="item">hahah</li>
          <li class="item">hahah</li>
        </ul>
      </section>
    </div>
  </div>
</template>

<script>


export default {
  name: 'app',
  components: {

  }
}
</script>

<style lang="scss">
  @import './assets/css/common.scss';
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
    }
    input{
      &.todo{
        height: 32px;
        width: 400px;
        border: none;
        outline: none;
        padding: 0px 16px 0 16px;
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
          #toggle + label{
            background-color: white;
            border-radius: 4px;
            border:1px solid #d3d3d3;
            width:20px;
            height:20px;
            display: inline-block;
            text-align: center;
            vertical-align: middle;
            line-height: 20px;
            margin-top: -2px;
          }
          #toggle:checked + label{
            background-color: #fff;
          }
          #toggle:checked + label:after{
            content:"\2714";
            color: #999;
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
