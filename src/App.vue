<template>
	<div id="app">
		<img alt="Vue logo" src="./assets/logo.png" />
		<!-- <p :style="ss">{{ hello }}</p>
		<p v-bind:style="ss">{{ hello }}</p>
		<h4 v-if="isLogin">로그인 하세요.</h4>
		<div v-for="(post, i) in posts" :key="i">
			<h4>{{ post.title }}</h4>
			<p>{{ post.date }} 발행</p>
		</div>
		<button type="button" class="btn btn-dark">Dark</button> -->
		<div class="container">
			<div class="row">
				<div class="col-md-2">
					<ul class="list-group mt-4">
						<li class="list-group-item">
							원래대로
						</li>
						<li class="list-group-item" v-on:click="sortPrice">
							가격순
						</li>
						<li class="list-group-item" v-on:click="sortName">
							가나다순
						</li>
					</ul>
				</div>
				<div class="col-md-10">
					<div class="row">
						<!-- 보내는이름="보낼데이터" -->
						<!-- <div v-for="item in Data" :key="item.id">
							<Card :data="item" />
						</div> -->
						<Card v-for="(data, i) in Data" :key="i" :data="data" />
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import Card from './components/Card';
import Data from './assets/data.js';

export default {
	name: 'App',
	data() {
		return {
			Data,
			hello: '안녕하세요. 반갑습니다.',
			ss: 'color: red',
			isLogin: false,
			posts: [
				{
					title: '오늘의 일기',
					date: '4월 20일',
				},
				{
					title: '수분크림 추천',
					date: '3월 4일',
				},
				{
					title: '강남 맛집 후기',
					date: '2월 22일',
				},
			],
		};
	},
	components: {
		Card,
	},
	methods: {
		sortPrice() {
			this.Data.sort(function(a, b) {
				return a.price - b.price;
			});
		},
		sortName() {
			this.Data.sort();
		},
	},
	watch: {
		Data() {
			console.log(111111);
		},
	},
	mounted() {},
};
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
