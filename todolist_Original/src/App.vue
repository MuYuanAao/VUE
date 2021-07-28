<template>
  <div id="root">
  <div class="todo-container">
    <div class="todo-wrap">
      <UserHeader :addMatter="addMatter"/>
      <UserList :matters="matters" :checkMatter="checkMatter" :deleteMatter="deleteMatter"/>
      <UserFooter :matters="matters" :checkAllMatter="checkAllMatter" :clearAllmatter="clearAllmatter"/>
    </div>
  </div>
</div>
</template>

<script>
import UserHeader from './components/UserHeader.vue'
import UserFooter from './components/UserFooter.vue'
import UserList from './components/UserList.vue'

export default {
  name: 'App',
  components:{UserHeader,UserFooter,UserList},
  data() {
    return {
      matters:JSON.parse(localStorage.getItem('matters')) || []
    }
  },
  methods: {
    //添加一个matter
    addMatter(matterObj){
      this.matters.unshift(matterObj)
    },
    //勾选或者取消勾选matter
    checkMatter(id){
      this.matters.forEach((matter) => {
            if(matter.id === id) matter.done = !matter.done
      })
    },
    //删除一个matter
    deleteMatter(id){
      this.matters=this.matters.filter((matter)=>{
        return matter.id != id
      })
    },
    //全选or取消全选
    checkAllMatter(done){
      this.matters.forEach((matter)=>{
        matter.done = done
      })
    },
    //清除所有已完成的matter
    clearAllmatter(){
      this.matters=this.matters.filter((matter)=>{
        return !matter.done
      })
    }
  },
  watch:{
    matters:{
        deep:true,
        handler(value){
          localStorage.setItem('matters',JSON.stringify(value))
        }
    }
    }
  }
</script>

<style>
	/*base*/
	body {
		background: #fff;
	}
	.btn {
		display: inline-block;
		padding: 4px 12px;
		margin-bottom: 0;
		font-size: 14px;
		line-height: 20px;
		text-align: center;
		vertical-align: middle;
		cursor: pointer;
		box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
		border-radius: 4px;
	}
	.btn-danger {
		color: #fff;
		background-color: #da4f49;
		border: 1px solid #bd362f;
	}
	.btn-danger:hover {
		color: #fff;
		background-color: #bd362f;
	}
	.btn:focus {
		outline: none;
	}
	.todo-container {
		width: 600px;
		margin: 0 auto;
	}
	.todo-container .todo-wrap {
		padding: 10px;
		border: 1px solid #ddd;
		border-radius: 5px;
	}
</style>
