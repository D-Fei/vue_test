<template>
  <div id="app">
	<div>
		<router-link to="/">首页</router-link>
		<router-link to="/about">关于我们</router-link>
	</div>
	<div>
		<router-view></router-view>
	</div>
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
	
	<!-- 打印信息 -->
	<div>{{ message1 }}</div>
	<!-- v-bind 动态绑定 -->
	<div>
		<span v-bind:title="message2">
			鼠标悬停几秒钟查看此处动态绑定的提示信息！
		</span>
	</div>
	<!-- v-if -->
	<div>
		<p v-if="seen">现在你看到我了</p>
		<p v-if="seen2">now you see me</p>
	</div>
	<!-- v-for循环 -->
	<div>
		<ol>
			<li v-for="todo in todos" v-bind:key="todo.id">
				{{ todo.text }}
			</li>
		</ol>
	</div>
	<!-- v-on -->
	<div>
		<p>{{ message1 }}</p>
		<button v-on:click="reverseMessage">反转消息</button>
	</div>
	<!-- v-model表单输入绑定 -->
	<div id="app-6">
		<p>{{ message1 }}</p>
		<input v-model="message1">
	</div>
	<!-- 组件 -->
	<div>
		<ol>
			<!--
			现在我们为每个 todo-item 提供 todo 对象
			todo 对象是变量，即其内容可以是动态的。
			我们也需要为每个组件提供一个“key”，稍后再
			作详细解释。
			-->
			<todoitem
			v-for="item in groceryList"
			v-bind:todo="item"
			v-bind:key="item.id"
			></todoitem>
		</ol>
	</div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import todoitem from './components/todo-item.vue'

export default {
  name: 'App',
  props: {
	message1:{
		type : String,
		default : 'Hello Vue!'
	},
	message2 : {
		type : String,
		default : '页面加载于 ' + new Date().toLocaleString()
	},
	seen : {
		type : Boolean,
		default : false
	},
	seen2 : {
		type : Boolean,
		default : true
	},
	groceryList : {
		type : Array,
		default : function(){
			return [
				{text:'蔬菜'},
				{text:'奶酪'},
				{text:'随便其它什么人吃的东西'}
			]
		}
	}
  },
  components: {
    HelloWorld,
	todoitem
  },
  methods: {
    reverseMessage: function () {
      this.message1 = this.message1.split('').reverse().join('')
    }
  },
  data(){
	return {
		todos:	[
					{ text: '学习 JavaScript' },
					{ text: '学习 Vue' },
					{ text: '整个牛项目' }
				]
	}	
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
