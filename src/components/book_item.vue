<template>
    <div class="book-item">
        <img class="back-img" :src="info.back_img" :alt="info.title">
        <div class="info">
            <img class="thum" :src="info.thum" :alt="info.title">
            <div class="title" v-text="info.title"></div>
            <div class="price" v-text="'￥' + info.price"></div>
            <div class="desc" v-text="info.desc"></div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'book-item',
        props: ['info']
    }
</script>

<style scoped="scoped">
    .book-item {
        margin-bottom: 20px;
    }
    img {
        display: block;
    }
    .back-img {
        width: 100%;
    }
    .info {
        background-color: #ffffff;
        padding: 20px 20px 20px 260px;
        position: relative;
    }
    .thum {
        width: 200px;
        position: absolute;
        top: -80px;
        left: 30px;
    }
    .title {
        font-size: 38px;
        color: #494949;
        line-height: 52px;
        font-weight: bold;
        margin-bottom: 20px;
    }
    .price {
        font-size: 28px;
        color: #e76648;
        margin-bottom: 20px;
    }
    .desc {
        font-size: 28px;
        color: #666666;
        overflow: hidden;      
        text-overflow: ellipsis;      
        display: -webkit-box; /* 将对象作为弹性伸缩盒子模型显示 */      
        -webkit-line-clamp: 3; /* 控制最多显示几行 */      
        -webkit-box-orient: vertical; /* 设置或检索伸缩盒对象的子元素的排列方式 */   
    }
</style>
