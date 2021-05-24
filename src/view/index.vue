<template>
    <div class="index">
        <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
            <van-swipe-item v-for="item in swiper_data" :key="item.link">
                <img class="swiper-img" :src="item.img" :alt="item.book_name">
            </van-swipe-item>
        </van-swipe>
        <van-tabs v-model="activeName" sticky color="#e76648" title-inactive-color="#9b9b9b" animated :before-change="beforeChange">
            <van-tab title="热门" name="1">
                <van-pull-refresh v-model="refreshing1" @refresh="onRefresh">
                    <van-list
                      v-model="loading1"
                      :finished="finished1"
                      finished-text="没有更多了"
                      @load="get_book_list"
                    >
                        <bookItem v-for="item in hot_book_list" :key="item.id" :info="item"></bookItem>
                    </van-list>
                </van-pull-refresh>
            </van-tab>
            <van-tab title="新书" name="2">
                <van-pull-refresh v-model="refreshing2" @refresh="onRefresh">
                    <van-list
                      v-model="loading2"
                      :finished="finished2"
                      finished-text="没有更多了"
                      @load="get_book_list"
                    >
                        <bookItem v-for="item in new_book_list" :key="item.id" :info="item"></bookItem>
                    </van-list>
                </van-pull-refresh>
            </van-tab>
        </van-tabs>
    </div>
</template>

<script>
    import bookItem from '@/components/book_item.vue'
    export default {
        name: 'index',
        components: {
            bookItem
        },
        data () {
            return {
                swiper_data: [
                    {link: '/detail/1', img: require('../assets/7847.jpg'), book_name: '重走'},
                    {link: '/detail/2', img: require('../assets/7847.jpg'), book_name: '重走'},
                    {link: '/detail/3', img: require('../assets/7847.jpg'), book_name: '重走'},
                    {link: '/detail/4', img: require('../assets/7847.jpg'), book_name: '重走'},
                    {link: '/detail/5', img: require('../assets/7847.jpg'), book_name: '重走'}
                ],
                hot_book_list: [],
                new_book_list: [],
                activeName: '1',
                loading1: false,
                loading2: false,
                refreshing1: false,
                finished1: false,
                finished2: false,
                refreshing2: false
            }
        },
        methods: {
            beforeChange (index) {
                if (index == 1 && this.loading2) {
                    return false
                }
                if (index == 2 && this.loading1) {
                    return false
                }
                return new Promise((resolve) => {
                    // 在 resolve 函数中返回 true 或 false
                    resolve(true);
                });
            },
            get_book_list () {
                if (this.activeName == 1) {
                    if (this.refreshing1) {
                        this.hot_book_list = [];
                        this.refreshing1 = false;
                    }
                } else {
                    if (this.refreshing2) {
                        this.new_book_list = [];
                        this.refreshing2 = false;
                    }
                }
                
                var item = {
                    title: '世界金奖级插画艺术家系列',
                    desc: '当我们置身于美术馆时，说起油画，我们会聊到凡高和莫奈。当我们身处充满设计感的空间，说起建筑，我们会谈论库哈斯和贝聿铭。当我们说起雕塑，我们会推崇米开朗基罗和贝尔尼尼。',
                    back_img: require('../assets/7956.jpg'),
                    thum: require('../assets/7953.jpg'),
                    price: '343'
                }
                setTimeout(() => {                    
                    for (var i = 0; i < 10; i++) {
                        var id = 'v' + parseInt(Math.random() * 100000000)
                        var book = {...item}
                        book.id = id
                        this[this.activeName == '1' ? 'hot_book_list' : 'new_book_list'].push(book)
                    }
                    this[this.activeName == '1' ? 'loading1' : 'loading2'] = false
                    if (this[this.activeName == '1' ? 'hot_book_list' : 'new_book_list'].length >= 40) {
                        this[this.activeName == '1' ? 'finished1' : 'finished2'] = true
                    }
                }, 1000)
            },
            onRefresh () {
                if (this.activeName == 1) {
                    // 清空列表数据
                    this.finished1 = false;
                    // 重新加载数据
                    // 将 loading 设置为 true，表示处于加载状态
                    this.loading1 = true;
                    this.get_book_list();
                } else {
                    // 清空列表数据
                    this.finished2 = false;
                    // 重新加载数据
                    // 将 loading 设置为 true，表示处于加载状态
                    this.loading2 = true;
                    this.get_book_list();
                }
                
            }
        }
    }
</script>

<style scoped>
    .swiper-img {
        width: 100%;
        display: block;
    }
</style>