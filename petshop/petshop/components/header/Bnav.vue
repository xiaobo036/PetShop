<template>
    <div class="el-bnav">
        <div class="el-brand">
            <div class="el-bar">欢迎访问宠物用品商城！</div>
            <div class="wf_td" v-if="!user.no">
                <nuxt-link to="/login" class="business">登录</nuxt-link>
                <nuxt-link to="/register" class="business">注册</nuxt-link>
            </div>
            <div v-else class="wf_td user">
                <span class="name" @click="handle">欢迎{{ user.nickname }}</span>
                <div class="ul" v-if="show">
                    <div @click="person">个人资料</div>
                    <div @click="person">我的订单</div>
                    <div @click="exit">退出登录</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
const router = useRouter()
const { user } = useCount()
const show = ref(false)
const handle = () => {
    show.value = !show.value
}
const person = () => {
    router.push('/person')
}
// 退出登录
const exit = async () => {
    const { data } = await useFetch('http://110.42.190.78:8888/api/user/exit');
    user.value = {}
    router.push('/')
}
</script>
<style  lang="scss">
@import "@/assets/css/header/bnav.scss";
.name {
    font-size: 12px;
    color: #666;
    cursor: pointer;
}
.user {
    font-size: 14px;
}

.ul {
    margin: 0;
    background-color: #fff;
    div {
        font-size: 12px;
        color: #666;
        padding: 3px;
        cursor: pointer;
        color: rgb(255, 144, 3);
    }
}
</style>