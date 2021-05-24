<template>
    <div id="app">
        <router-view/>
    </div>
</template>

<script>
    export default {
        name: 'App'
    }
</script>

<style>
    * {
        margin: 0;
        padding: 0;
    }
    body {
        background-color: #F7F1ED;
    }
    img {
        content: normal !important;
    }
    .van-tab__pane {
        padding: 10px 0;
    }
</style>
