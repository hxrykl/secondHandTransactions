<style>
    #customers .el-row button{
        float: right;
        margin:0px 15px 10px 0px;
        color: #fff;
    }
    #customers .el-row button:hover{
        background-color: #535bd0;
        border-color: #535bd0;
    }
    #customers .el-form-item {
        margin-bottom: 0px;
    }
    #customers .el-form-item > div.el-form-item__content{
        line-height: 32px;
    }
    
</style>
<template>
    <!-- 顾客管理模块 -->
    <div id="customers">
        <!-- 操作按钮 -->
        <el-row>
            <!-- 搜索 -->
            <el-col :span="8">
                <!-- 输入搜索内容 -->
                <el-form :inline="true">
                    <el-form-item>
                        <el-input style="margin-bottom: 10px;" v-model="input" size="small" placeholder="请输入关键字"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <!-- 搜索按钮 -->
                        <el-button size="small" type="primary">搜索</el-button>
                    </el-form-item>
                </el-form>
                <!-- 输入搜索内容结束 -->
            </el-col>
            <!-- 搜索结束 -->
            <!-- 删除/添加/全选数据 -->
            <el-col :span="16">
                <el-button size="small" type="primary">删除</el-button>
                <el-button size="small" type="primary">全选</el-button>
                <el-button size="small" type="primary">添加</el-button>
            </el-col>
            <!-- 删除/添加/全选数据结束 -->
        </el-row>
        <!-- 操作按钮结束 -->
        <!-- 数据显示表格 -->
        {{categories}}
        <el-table :data="categories" style="width: 100%">
            <!-- 编号 -->
            <el-table-column prop="id" label="编号" width="180"></el-table-column>
            <!-- 姓名 -->
            <el-table-column prop="realname" label="姓名" width="180"> </el-table-column>
            <!-- 手机号 -->
            <el-table-column prop="telephone" label="手机号"> </el-table-column>
            <!-- 状态 -->
            <el-table-column prop="status" label="状态"> </el-table-column>
            <!-- 操作 -->
            <el-table-column label="操作">
                <template v-slot:default="scope">
                    <a href="" @click.prevent="deleteHandler(scope.row.id)">删除</a>
                    <a href="" @click.prevent="deleteHandler(scope.row)">修改</a>
                </template>
            </el-table-column>
            <!-- 操作结束 -->
        </el-table>
        <!-- 数据显示表格结束 -->
        <!-- 分页 -->
        <el-pagination small layout="prev, pager, next" :total="50">
        </el-pagination>
        <!-- 分页结束 -->
    </div>
    <!-- 顾客管理模块结束 -->
</template>
<script>
//依赖模块
import {post} from "../http/axios"//eport暴露成员用{}接收,其中就有get变量


// 默认组件
export default { 
    data() {
        return {
            title: "顾客管理",
            customers: [],
            input: "",
            params:{
                page:0,
                pageSize:5
            },
            categories:[]
        }
    },
    methods: {
        async loadData(){
            let response = await post("/customer/query",this.params);
            this.categories = response.data;
            alert(1);
        },
        deleteHandler(id) {
            this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
                    confirmButtonText: '确定',
                    cancelButtonText: '取消',
                    type: 'warning'
                }).then(() => {
                    //执行删除
                    axios.get("/customer/deleteById", { params: { id } })
                        .then((response) => {
                            this.$message({
                                type: 'success',
                                message: 'response.data.message'
                            });
                        })

                })
                .catch(() => {
                    this.$message({
                        type: 'info',
                        message: '已取消删除'
                    });
                });
        }
    }
}
</script>