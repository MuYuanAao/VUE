<template>
    <div class="todo-footer" v-if="total">
        <label>
          <!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
          <input type="checkbox" v-model="isAll"/>
        </label>
        <span>
          <span>已完成{{doneTotal}}</span> / 全部{{total}}
        </span>
        <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
    </div>
</template>

<script>
export default {
    name:'UserFooter',
    props:['matters','checkAllMatter','clearAllmatter'],
    computed:{
      //总数
      total(){
        return this.matters.length
      },
      //已完成数
      doneTotal(){
        //此处使用reduce方法做条件统计
				/* const x = this.todos.reduce((pre,current)=>{
					console.log('@',pre,current)
					return pre + (current.done ? 1 : 0)
				},0) */
				//简写
        return this.matters.reduce((pre,matter) => pre + (matter.done ? 1 : 0),0)
      },
      //控制全选框
      isAll:{
        //是否勾选
        // return this.total === this.doneTotal && this.total >0
        get(){
          return this.total === this.doneTotal && this.total >0
        },
        //isAll被修改时set被调用
        set(value){
          this.checkAllMatter(value)
        }
      },
    },
    methods: {
      // checkAll(e){
      //   console.log(e.target.checked)
      //   this.checkAllMatter(e.target.checked)
      // },
      //清楚所有已完成
      clearAll(){
        this.clearAllmatter()
      }
    },
}
</script>

<style scoped>
	/*footer*/
	.todo-footer {
		height: 40px;
		line-height: 40px;
		padding-left: 6px;
		margin-top: 5px;
	}

	.todo-footer label {
		display: inline-block;
		margin-right: 20px;
		cursor: pointer;
	}

	.todo-footer label input {
		position: relative;
		top: -1px;
		vertical-align: middle;
		margin-right: 5px;
	}

	.todo-footer button {
		float: right;
		margin-top: 5px;
	}
</style>