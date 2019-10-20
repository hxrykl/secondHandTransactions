<template>
    <div id="app">
        <el-row>
            <el-col :span="4" style="background-color: #8378e5;color: #fff;">
                <div class="grid-content bg-purple">
                    <h2 style="text-align: center;">{{title}}</h2>
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
            <el-col :span="20">
                <div class="grid-content bg-purple-light">
                    <div style="height: 60px;" id="crumbs">
                        <el-breadcrumb separator="/">
                            <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
                            <el-breadcrumb-item>{{arrTitle[num]}}</el-breadcrumb-item>
                        </el-breadcrumb>
                    </div>
                    <div style="padding: 30px;background-color: #eaecee91;">
                        <component :is="currentPage"></component>
                    </div>
                </div>
            </el-col>
        </el-row>
    </div>
</template>
<script>
import Sort from './pages/Sort' //栏目管理
import Customer from './pages/Customer' //顾客管理
import Address1 from './pages/Address1' //地址管理
import Attendant from './pages/Attendant' //服务员管理
import Product from './pages/Product' //产品管理
import Evaluate from './pages/Evaluate' //评价管理


export default {
    name: 'app',
    data() {
        return {
            title: "二手交易系统",
            currentPage: "Customer",
            num: "4",
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
                clickLi: {
                    "color": "#fff"
                }
            }
        };
    },
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