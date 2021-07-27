<template>
    <ul class="todo-main">
        <Item 
        v-for="matterObj in matters" 
        :key="matterObj.id" 
        :matter="matterObj"
        :checkMatter="checkMatter"
        :deleteMatter="deleteMatter"
        />
    </ul>
</template>

<script>
import Item from './Item.vue'

export default {
    name:'UserList',
    components:{Item},
    props:['matters','checkMatter','deleteMatter']
}
</script>

<style scoped>
	/*main*/
	.todo-main {
		margin-left: 0px;
		border: 1px solid #ddd;
		border-radius: 2px;
		padding: 0px;
	}

	.todo-empty {
		height: 40px;
		line-height: 40px;
		border: 1px solid #ddd;
		border-radius: 2px;
		padding-left: 5px;
		margin-top: 10px;
	}
</style>