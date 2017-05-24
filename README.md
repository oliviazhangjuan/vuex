# Vuex -- 状态管理模式
### 状态管理模式
- state,驱动应用的数据源
- view,以声明方式将state映射到视图
- actions,响应在view上的用户输入导致的状态变化

### Store
- store(仓库,容器),每个Vuex应用的核心,包含着应用中大部分的**状态**(state)
1. 响应式的
2. 改变的唯一途径--显示提交(commit)mutations

```javascript
const store = new Vuex.Store({
	 state:{
	 	count: 0
	 },
	 mutations:{
	 	increment(state){
	 		state.count++
	 	}
	 }
})
//获取对象及触发状态变更
store.commit('increment');
alert(store.state.count) -> 1
//组件调用,先在根实例中注册store
computed:{
	 count:function(){
	 	 return this.$store.state.count
	 }
}
//使用辅助函数mapState
computed:{
	 total:function(){//局部计算属性
	 	 return .....
	 },
	 ...mapState({
	 	 count: state => state.count
	 })
}
```
### Getters
从store中的state中派生出一些状态,供多个组件使用

```javascript
//state.js
const store = new Vuex.Store({
	 state: {
	 	........
	 },
	 getters:{
	 	 price: (state, getters) => {
		 	 .....
		 }
	 }
})
//组件中使用
computed:{
	 price:function(){
	 	 return this.$store.getters.price
	 }
}
//使用辅助函数mapGetters
computed:{
     //局部计算属性
	 .......,
	 ...mapGetters([
	 	 'a',
	 	 'b'
	 ])
}
```
### Mutations
- 更改Vuex中的状态的唯一方法是提交mutations
- 每个mutation都有一个字符串的**事件类型(type)**和一个**回调函数(handler)**
- 回调函数就是实际进行状态更改的地方，并接受state作为第一参数
- mutation必须是同步函数
