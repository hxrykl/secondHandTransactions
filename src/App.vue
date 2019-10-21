<template>
    <!-- 最大容器 -->
    <div id="app">
        <!-- 伸缩盒子布局 -->
        <el-row>
            <!-- 左边导航栏 -->
            <el-col :span="4" style="background-color: #8378e5;color: #fff;">
                <div class="grid-content bg-purple">
                    <!-- logo -->
                    <h2 style="text-align: center;">{{title}}</h2>
                    <!-- 菜单栏 -->
                    <ul style="float: left;width: 200px;font-size: 20px;padding-left: 30px;">
                        <li @click="currentPage = 'Product';num = '1'" :style="num == 1?style.clickLi:{}">
                            产品管理
                            <span v-show="num == 1">></span>
                        </li>
                        <li @click="currentPage = 'Sort';num = '2'" :style="num==2?style.clickLi:{}">
                            栏目管理
                            <span v-show="num == 2">></span>
                        </li>
                        <li @click="currentPage = 'Evaluate';num = '3'" :style="num==3?style.clickLi:{}">
                            评价管理
                            <span v-show="num == 3">></span>
                        </li>
                        <li @click="currentPage = 'Customer';num = '4'" :style="num==4?style.clickLi:{}">
                            顾客管理
                            <span v-show="num == 4">></span>
                        </li>
                        <li @click="currentPage = 'Attendant';num = '5'" :style="num==5?style.clickLi:{}">
                            服务员管理
                            <span v-show="num == 5">></span>
                        </li>
                        <li @click="currentPage = 'Address1';num = '6'" :style="num==6?style.clickLi:{}">
                            地址管理
                            <span v-show="num == 6">></span>
                        </li>
                    </ul>
                </div>
            </el-col>
            <!-- 右边内容 -->
            <el-col :span="20">
                <div class="grid-content bg-purple-light">
                    <!-- 头部 -->
                    <div style="height: 60px;" id="crumbs">
                        <!-- 面包屑导航 -->
                        <el-breadcrumb separator="/">
                            <!-- 返回首页 -->
                            <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
                            <!-- 子模块名 -->
                            <el-breadcrumb-item>{{arrTitle[num]}}</el-breadcrumb-item>
                        </el-breadcrumb>
                    </div>
                    <!-- 内容 -->
                    <div style="padding: 30px;background-color: #eaecee91;">
                        <!-- 子页面导入 -->
                        <component :is="currentPage"></component>
                    </div>
                </div>
            </el-col>
        </el-row>
    </div>
</template>
<script>
//绑定子模块地址
import Sort from './pages/Sort' //栏目管理
import Customer from './pages/Customer' //顾客管理
import Address1 from './pages/Address1' //地址管理
import Attendant from './pages/Attendant' //服务员管理
import Product from './pages/Product' //产品管理
import Evaluate from './pages/Evaluate' //评价管理

// 默认组件
export default {
    name: 'app',
    data() {
        return {
            // logo
            title: "二手交易系统",
            // 引入的子模块
            currentPage: "Customer",
            // 绑定子模块
            num: "4",
            // 子模块面包屑
            arrTitle:[
              "标题",
              "产品管理",
              "栏目管理",
              "评价管理",
              "顾客管理",
              "服务员管理",
              "地址管理"
            ],

            style: {
                // 点击菜单栏的样式
                clickLi: {
                    "color": "#fff"
                }
            }
        };
    },
    // 子模块引用
    components: {
        Address1,
        Customer,
        Sort,
        Evaluate,
        Product,
        Attendant
    }


}
</script>
<!-- 样式 -->
<style>

html,
body,
#app,
#app>div,
#app>div>div {
    margin: 0;
    height: 100%;
}

#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    color: #2c3e50;
}

#app>div>div ul {
    list-style: none;
    margin: 0;
    padding: 0;
}

#app>div>div ul>li {
    padding: 10px 0;
    color: #d3d3d3;
}

#app div li span {
    float: right;
    padding-right: 45px;
}
#crumbs span{
  line-height: 60px;
  font-size: 18px;
}
</style>