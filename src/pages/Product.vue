<style>
    #product .el-row button{
        float: right;
        margin:0px 15px 10px 0px;
        color: #fff;
    }
    #product .el-row button:hover{
        background-color: #535bd0;
        border-color: #535bd0;
    }
    #product .el-form-item {
        margin-bottom: 0px;
    }
    #product .el-form-item > div.el-form-item__content{
        line-height: 32px;
    }
    
</style>
<template>
    <!-- 产品管理模块 -->
    <div id="product">
        <!-- 操作按钮 -->
        <el-row>
            <!-- 搜索 -->
            <el-col :span="8">
                <!-- 输入搜索内容 -->
                <el-form :inline="true">
                    <el-form-item>
                        <el-input @change="loadData" style="margin-bottom: 10px;" v-model="params.name" size="small" placeholder="请输入名字"></el-input>
                    </el-form-item>
                    <el-form-item>
                        <!-- 搜索按钮 -->
                        <el-button @click="loadData" size="small" type="primary">搜索</el-button>
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
        <el-table :data="produts.list" style="width: 100%;height: 428px;">
            <!-- 编号 -->
            <el-table-column prop="id" label="编号" width="80"></el-table-column>
            <!-- 姓名 -->
            <el-table-column prop="name" label="产品名" width="120"> </el-table-column>
            <!-- 类别 -->
            <el-table-column prop="category.name" label="类别" width="100"> </el-table-column>
            <!-- 价格 -->
            <el-table-column prop="price" label="价格" width="100"> </el-table-column>
            <!-- 产品图 -->
            <el-table-column prop="photo" label="产品图" width="360"> </el-table-column>
            <!-- 描述 -->
            <el-table-column prop="description" label="描述" width="240"> </el-table-column>、
            <!-- 状态 -->
            <el-table-column prop="status" label="状态" width="100"> </el-table-column>
            <!-- 操作 -->
            <el-table-column label="操作">
                <!-- #default -->
                <template #default="record">
                    <a href="" @click.prevent="toDetail(record)">详情</a>
                </template>
            </el-table-column>
            <!-- 操作结束 -->
        </el-table>
        <!-- 数据显示表格结束 -->
        <!-- 分页 -->
        <el-pagination style="text-align: center;" @current-change="pageChangeHandler" layout="prev, pager, next" :current-page="params.page+1" :page-size="produts.pageSize" :total="produts.total">
        </el-pagination>
        <!-- 分页结束 -->
        <!-- 模态框 -->
        <el-dialog title="添加产品信息" :visible.sync="dialogVisible">
            <el-form :model="form">
            	<!-- label-width为活动名称宽度 -->
                <el-form-item label="活动名称" :label-width="formLabelWidth">
                    <el-input v-model="form.name" autocomplete="off"></el-input>
                </el-form-item>
                <el-form-item label="活动区域" :label-width="formLabelWidth">
                    <el-select v-model="form.region" placeholder="请选择活动区域">
                        <el-option label="区域一" value="shanghai"></el-option>
                        <el-option label="区域二" value="beijing"></el-option>
                    </el-select>
                </el-form-item>
            </el-form>
            <div slot="footer" class="dialog-footer">
                <el-button @click="dialogFormVisible = false">取 消</el-button>
                <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
            </div>
        </el-dialog>
        <!-- 模态框结束 -->
    </div>
    <!-- 产品管理模块结束 -->
</template>
<script>
//依赖模块
import { post } from "../http/axios" //eport暴露成员用{}接收,其中就有get变量


// 默认组件
export default {
    data() {
        return {
            title: "产品管理",
            dialogVisible:false,
            params: {
                page: 0,
                pageSize: 6,
                namereal: ""
            },
            produts: [],
            // record: "",
            form:{}
        }
    },
    created() {
        this.loadData();
    },
    methods: {
        // 测试用
        lo() {
            alert(1);
        },
        //看详情方法
        toDetail() {
            console.log(this.record);
        },
        //分页处理方法
        pageChangeHandler(currentPage) {
            this.params.page = currentPage - 1;
            this.loadData();
        },
        //获取分页数据方法
        async loadData() {
            let response = await post("/product/queryProductCascadeCategory", this.params);
            this.produts = response.data;
            console.log(this.params);
        },
        //
        deleteHandler(id) {
            this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
                    confirmButtonText: '确定',
                    cancelButtonText: '取消',
                    type: 'warning'
                }).then(() => {
                    //执行删除
                    axios.get("/product/deleteById", { params: { id } })
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