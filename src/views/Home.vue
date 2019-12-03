<template>
  <div class="home">
  	<form @submit.prevent="addTodo">
  		<label for="newTodo">New Todo</label>
  		<input v-model="newTodo" type="text" name="newTodo">
  		<button type="submit">Add</button>
  	</form>
  	<button @click="allDone">All Done</button>
    <ul>
    	<li v-for="(todo,index) in todos" :key="todo.id">
    		<input @click="toggleTodoDone(index)" type="checkbox" :checked="todo.done">
    	<span :class="{done:todo.done}">{{todo.title}}</span>
    	</li>
    </ul>
  </div>
</template>

<script>
// @ is an alias to /src
import { mapState, mapActions, mapMutations } from 'vuex';

export default {
  name: 'home',
  computed: {
  	newTodo:{
  		get(){
  			return this.$store.state.newTodo;
  		},
  		set(value){
  			this.$store.commit('setNewTodo',value);
  		}
  	},
  	...mapState(['todos'])
  },
  methods:{
  	...mapActions(['addTodo','toggleTodoDone']),
  	...mapMutations(['allDone'])
  }

}
</script>
<style>
	.done{
		text-decoration: line-through;
	}
</style>
