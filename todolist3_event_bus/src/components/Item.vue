<template>
    <li>
        <label>
        <input type="checkbox" :checked="matter.done" @change="handleCheck(matter.id)"/>
        <span>{{matter.title}}</span>
        </label>
        <button class="btn btn-danger" @click="handleDelete(matter.id)">删除</button>
    </li>
</template>

<script>
export default {
    name:'Item',
    //声明接收
    props:['matter'],
    methods: {
      //勾选或取消勾选
      handleCheck(id){
        //通知App组件将对应的matter对象的done值取反
        // this.checkMatter(id)
		this.$bus.$emit('checkMatter',id)
      },
      //删除
      handleDelete(id){
        if(confirm('真的要删除吗')){
          //通知App组件将对应的matter对象删除
          //this.deleteMatter(id)
		this.$bus.$emit('deleteMatter',id)
        }
      }
  }
}
</script>

<style scoped>
	/*item*/
	li {
		list-style: none;
		height: 36px;
		line-height: 36px;
		padding: 0 5px;
		border-bottom: 1px solid #ddd;
	}

	li label {
		float: left;
		cursor: pointer;
	}

	li label li input {
		vertical-align: middle;
		margin-right: 6px;
		position: relative;
		top: -1px;
	}

	li button {
		float: right;
		display: none;
		margin-top: 3px;
	}

	li:before {
		content: initial;
	}

	li:last-child {
		border-bottom: none;
	}

	li:hover{
		background-color: #ddd;
	}
	
	li:hover button{
		display: block;
	}
</style>