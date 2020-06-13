<template>
    <div id="app">
        <img alt="Vue logo" src="./assets/logo.png"/>
        <!-- <p :style="ss">{{ hello }}</p>
        <p v-bind:style="ss">{{ hello }}</p>
        <h4 v-if="isLogin">로그인 하세요.</h4>
        <div v-for="(post, i) in posts" :key="i">
            <h4>{{ post.title }}</h4>
            <p>{{ post.date }} 발행</p>
        </div>
        <button type="button" class="btn btn-dark">Dark</button> -->
        <transition name="wow">
            <div v-if="viewModal" class="container my-modal">
                <div class="row">
                    <div class="col-md-6">
                        <img :src="Data[clickIndex].image" alt="" width="70%" />
                    </div>
                    <div class="col-md-6">
                        <h4>{{Data[clickIndex].title}}</h4>
                        <p>가격: {{Data[clickIndex].price}}</p>
                        <input
                                v-on:click="computePrice"
                                v-model="totalMonth"
                                type="range"
                                class="form-control-range" min="0" max="12" >
                        <p>총 비용: {{totalPrice}}</p>
                        <button class="btn btn-danger" v-on:click="viewModal=false">닫기</button>
                    </div>
                </div>
            </div>
        </transition>
        <ul>
            <button>버튼1</button>
            <button>버튼2</button>
            <button>버튼3</button>
        </ul>
        <div>
            내용1
        </div>
        <div>내용2</div>
        <div>내용3</div>
        <div class="container">
            <div class="row">
                <div class="col-md-2">
                    <ul class="list-group mt-4">
                        <li class="list-group-item" v-on:click="sortOrigin">
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
                        <Card v-for="(data, i) in Data" :key="i" :data="data"
                                v-on:click.native="showModal(i, $event)"/>
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
                viewModal: false,
                clickIndex: 0,
                totalMonth: 0,
                totalPrice: 0
            };
        },
        components: {
            Card,
        },
        methods: {
            sortOrigin() {
                this.Data = [...Data];
            },
            sortPrice() {
                this.Data = this.Data.slice(0).sort((a, b) => a.price - b.price);
            },
            sortName() {
                this.Data = this.Data.slice(0).sort(function(a, b) {
                    const x = a.title.toLowerCase();
                    const y = b.title.toLowerCase();
                    return x < y ? -1 : x > y ? 1 : 0;
                });
            },
            showModal(index, e) {
                this.clickIndex = index;
                this.viewModal = true;
                e.preventDefault = false;
            },
            computePrice() {
                this.totalPrice = this.totalMonth * this.Data[this.clickIndex].price;
            }
        },
        watch: {
            Data() {
                console.log('watch');
            },
        },
        created() {
            console.log('created');
        },
        mounted() {
            console.log('mounted');
        },
    };
</script>

<style>
    .my-modal {
        position: fixed;
        width: 100%;
        height: 100%;
        background: white;
        padding: 30px;
        z-index: 10;
    }
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
    }
    .wow-enter {
        transform: translateX(100%);
        opacity: 0;
    }
    .wow-enter-to {
        transform: translateX(0%);
        opacity: 1;
    }
    .wow-enter-active {
        transition: all 0.5s;
    }
    .wow-leave {
        opacity: 1;
    }
    .wow-leave-to {
        opacity: 0;
    }
    .wow-leave-active {
        transition: all 0.5s;
    }
</style>
