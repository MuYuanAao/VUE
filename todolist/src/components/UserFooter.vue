<template>
    <div class="todo-footer" v-if="total">
        <label>
          <!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
          <input type="checkbox" v-model="isAll"/>
        </label>
        <span>
          <span>已完成{{doneTotal}}</span> / 全部{{total}}
        </span>
        <button class="btn btn-danger" @click="clearAllmatter">清除已完成任务</button>
    </div>
</template>

<script>
export default {
    name:'UserFooter',
    props:['matters','checkAllMatter','clearAllmatter'],
    computed:{
      total(){
        return this.matters.length
      },
      doneTotal(){
        return this.matters.reduce((pre,matter) => pre + (matter.done ? 1 : 0),0)
      },
      isAll:{
        // return this.total === this.doneTotal && this.total >0
        get(){
          return this.total === this.doneTotal && this.total >0
        },
        set(value){
          this.checkAllMatter(value)
        }
      },
    },
    methods: {
      checkAll(e){
        console.log(e.target.checked)
        this.checkAllMatter(e.target.checked)
      },
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