<style>
    #customers .el-row button{
        background-color: #747cf3;
        border-color:#747cf3;
        float: right;
        margin:0px 15px 10px 0px;
    }
    #customers .el-row button:hover{
        background-color: #535bd0;
        border-color: #535bd0;
    }
</style>
<template>
    <div id="customers">
        <el-row>
            <el-col :span="8">
                <div class="demo-input-suffix">
                    <el-button size="small" type="primary" icon="el-icon-search">搜索</el-button>
                    <el-input v-model="input" prefix-icon="el-icon-search" placeholder="请输入内容"></el-input>
                </div>
            </el-col>
            <el-col :span="16">
                <el-button size="small" type="primary">删除</el-button>
                <el-button size="small" type="primary">全选</el-button>
                <el-button size="small" type="primary">添加</el-button>
            </el-col>
        </el-row>
        <el-table :data="customers" style="width: 100%">
            <el-table-column prop="id" label="编号" width="180"></el-table-column>
            <el-table-column prop="realname" label="姓名" width="180"> </el-table-column>
            <el-table-column prop="telephone" label="手机号"> </el-table-column>
            <el-table-column prop="status" label="状态"> </el-table-column>
            <el-table-column label="操作">
                <template v-slot:default="scope">
                    <a href="" @click.prevent="deleteHandler(scope.row.id)">删除</a>
                    <a href="" @click.prevent="deleteHandler(scope.row)">修改</a>
                </template>
            </el-table-column>
        </el-table>
    </div>
</template>
<script>
import axios from "axios"
axios.defaults.baseURL = "http://39.105.108.131:6677";
// 响应拦截
axios.interceptors.response.use((response) => {
    if (response.data.status !== 200) {
        alert(response.data.message);
        return Promise.reject(error);
    }
    return response;
}, (error) => {
    alert(1);
    return Promise.reject(error);
})
export default {
    created() {
        axios.get("/customer/findAll")
            .then((response) => {
                //将查询的结果赋值为customers
                this.customers = response.data.data;
            })
    },
    data() {
        return {
            title: "顾客管理",
            customers: []
        }
    },
    methods: {
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