<template>
  <div class="todoList">
    <el-row class="content">
      <el-col :xs="{span:20,offset:2}" :sm="{span:8,offset:8}">
        <span>欢迎{{name}}!</span>
        <el-input v-model="todos" placeholder="请输入待办事项，按回车键添加" @keyup.enter.native="addTodos"></el-input>
        <el-tabs v-model="activeName" @tab-click="handleClick">
          <el-tab-pane label="待办事项" name="first">
            <el-col>
              <div v-if="Done">
                <div v-for="(item,index) in list">
                  <div class="todo-list" v-if="item.status == false">
                    <span class="item">
                      {{item.content}}
                    </span>
                    <span class="pull-right">
                      <el-button size="small" type="primary" @click="finished(index)">完成</el-button>
                      <el-button size="small" :plain="true" type="danger" @click="remove(index)">删除</el-button>
                    </span>
                  </div>
                </div>
              </div>
              <div v-else>
                暂无待办事项
              </div>
            </el-col>
          </el-tab-pane>
          <el-tab-pane label="已完成事项" name="second">
            <div v-if="count > 0">
              <div v-for="(item, index) in list">
                <div class="todo-list" v-if="item.status == true">
                <span class="item finished">
                   {{ item.content }}
                </span>
                  <span class="pull-right">
                  <el-button size="small" type="primary" @click="restore(index)">还原</el-button>
                </span>
                </div>
              </div>
            </div>
            <div v-else>
              暂无已完成事项
            </div>
          </el-tab-pane>
        </el-tabs>
      </el-col>
    </el-row>
  </div>
</template>
<style lang="stylus" scoped>
  .el-input
    margin 20px auto
  .todo-list
    width 100%
    margin-top 8px
    padding-bottom 8px
    border-bottom 1px solid #eee
    overflow hidden
    text-align left
    .item
      font-size 20px
      &.finished
        text-decoration line-through
        color #ddd
  .pull-right
    float right
</style>
<script>
    export default{
      data() {
        return {
          name: 'ZS',
          activeName: 'first',
          list: [{
            status:false,
            content:'121212'
          }],
          count: 0,
        };
      },
      created() {
        this.name = localStorage.getItem('account');
      },
      computed: {
        Done() {
          let count = 0;
          let length = this.list.length;
          for(let i in this.list){
            this.list[i].status == true ? count ++ : '';
          }
          this.count = count;
          if(count == length || length == 0){
            return false;
          }else{
            return true;
          }
        }
      },
      methods: {
          addTodos() {
            if(this.todos == '')
              return
            let obj = {
              status: false,
              content: this.todos
            }
            this.list.push(obj);
            this.$message({
                type: 'success',
                message: '添加成功'
            });
            this.todos = '';
          },
          finished(index) {
            //this.$set(this.list[index],'status',true) // 通过set的方法让数组的变动能够让Vue检测到
            this.list[index].status = true;
            this.$message({
              type: 'success',
              message: '任务完成'
            })
          },
          remove(index) {
            this.list.splice(index,1);
            this.$message({
              type: 'info',
              message: '任务删除'
            });
          },
          restore(index) {
            //this.$set(this.list[index],'status',false)
            this.list[index].status = false;
            this.$message({
              type: 'info',
              message: '任务还原'
            })
          }
        }
      }
</script>
