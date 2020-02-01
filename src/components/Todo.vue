<template>
  <div>
    <el-row type="flex" justify="center" class="row-container">
      <el-col :span="16" class="row-todo">
        <el-button @click="completeTodo" type="success" plain size="small" icon="el-icon-check" circle></el-button>
        {{ todoName }}
        <!-- <el-button-group class="button-group"> -->
          <!-- <el-button type="primary" plain size="small" icon="el-icon-edit" circle></el-button> -->
          <el-button @click="deleteTodo" class="delete-btn" type="danger" plain size="small" icon="el-icon-close" circle></el-button>
        <!-- </el-button-group> -->
      </el-col>
    </el-row>
  </div>
</template>

<script>
  export default {
    props: ['todoName', 'completed'],
    methods: {
      deleteTodo() {
        window.console.log('hit del');
        window.console.log(this.todoName);
        this.$emit('todo-deleted', this.todoName);
      },
      completeTodo() {
        this.$emit('todo-completed', this.todoName);
      }
    }
  }
</script>

<style>
  .row-todo {
    background: lightblue;
    border-radius: 6px;
    margin: 3px;
    padding: 5px;
    line-height: 2em;
  }
  .row-todo:hover {
    background: #2343ff;
  }
  .delete-btn {
    float: right;
  }

</style>
