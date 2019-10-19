<template>
	<section>
		<!--工具条-->
		<el-col :span="24" class="toolbar" style="padding-bottom: 0px;">
			<el-form :inline="true" :model="filters">
				<el-form-item>
					<el-input v-model="filters.num" type="number" placeholder="请输入"></el-input>
				</el-form-item>
				<el-form-item>
					<el-button type="primary" @click="testPromise">promise1测试</el-button>
				</el-form-item>
				<el-form-item>
					<el-button type="primary" @click="moreTextPromise">promise2测试</el-button>
				</el-form-item>
				<el-form-item>
					<el-button type="primary" @click="testAsyncFunction">aysnc测试</el-button>
				</el-form-item>
				<el-form-item>
					<el-button type="primary" @click="testAwaitFunction">await测试</el-button>
				</el-form-item>
			</el-form>
		</el-col>
	</section>
</template>

<script>
	import util from '../../common/js/util'
	//import NProgress from 'nprogress'
	import { getUserListPage, removeUser, batchRemoveUser, editUser, addUser } from '../../api/api';
	export default {
		data() {
			return {
				filters:{
					num:0
				}
			}
		},
		methods: {
			// promise测试
			// 当调用testPromise函数后，同步执行getdate方法，获取返回值后调用testPThen方法
			// promise是同步执行，主要解决函数多级调用，节省等待时间，让代码可读性更高，vue常用的axios就是在promise的基础上做了封装
			getdate(data) {
				return new Promise((resolve, reject)=>{
					if (data > 3) {
						resolve(data);
					} else {
						reject("小于或等于3");
					}
				});
			},
			testPThen(res) {
				console.log("=====", res)
			},
			// 调用
			testPromise() {
				this.getdate(this.filters.num).then((reDate)=>{
					this.testPThen(reDate);
				});
				this.getdate(this.filters.num).then((reDate)=>{
					this.testPThen(reDate);
				});
			},
			// 再比如
			getPromiseMore1(){
				var p = new Promise(function(resolve, reject){
					console.log(1)
				})
				return p;
			},
			getPromiseMore2(){
				var p = new Promise(function(resolve, reject){
					console.log(2)
				})
				return p;
			},
			moreTextPromise(){
				this.getPromiseMore1().then(
					this.getPromiseMore2()
				)
			},


			//aysnc测试
			async isAysnc(num) {
				if (num > 0) {
					// 这里相当于promise的resolve
					return num + '大于零'
				} else {
					// 这里相当于promise的reject
					throw num  + '小于等于0'
				}
			},

			testAsyncFunction(){
				this.isAysnc(this.filters.num).then(function (reDate) {
					console.log(reDate); 
				}),
				this.isAysnc(this.filters.num).catch(function (reDate) {
					console.log(reDate);
				})
			},

			//await测试，只能与aysnc同时使用
			// await会让同步执行的函数进入等待，一般使用的场合，后面的操作（B），必须要前面函数（A）获取的数据支持
			// 函数因为是同步执行，如果函数A获取数据还未执行完成，就执行函数B，就会出错，这种情况就可以使用await
			getSomething(num){
				for(let i = num;i > 0;i--){
					setTimeout(function(){
						console.log('先' + i)
					},1000)
				}
			},
			
			async testAsync(num){
				for(let i = num;i > 0;i--){
					setTimeout(function(){
						console.log('后' + i)
					},1000)
				}
			},
			
			async testAwaitFunction(){
				await this.getSomething(3);
				await this.testAsync(3);
			}
		},
	}


</script>