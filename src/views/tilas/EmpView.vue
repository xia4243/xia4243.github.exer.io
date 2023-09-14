<template>
    <div>
        <el-container style="height: 700px; border: 1px solid #eee">
            <el-header style="font-size:40px; background-color: rgb(238, 241, 246)">智能学习辅助系统</el-header>
            <el-container>
                <el-aside width="200px">
                    <el-menu :default-openeds="['1', '3']">
                        <el-submenu index="1">
                            <template slot="title"><i class="el-icon-message"></i>系统信息管理</template>

                            <el-menu-item index="1-1">
                                <router-link to="/emp">员工管理</router-link>
                            </el-menu-item>

                            <el-menu-item index="1-2">
                                <router-link to="/element">部门管理</router-link>
                            </el-menu-item>

                        </el-submenu>

                    </el-menu>
                </el-aside>
                <el-main>
                    <!-- 表单 -->
                    <el-form :inline="true" :model="formInline" class="demo-form-inline">
                        <el-form-item label="姓名">
                            <el-input v-model="formInline.user" placeholder="审批人"></el-input>
                        </el-form-item>
                        <el-form-item label="性别">
                            <el-select v-model="formInline.region" placeholder="活动区域">
                                <el-option label="男" value="1"></el-option>
                                <el-option label="女" value="2"></el-option>
                            </el-select>
                        </el-form-item>
                        <el-form-item label="入职日期">
                            <!-- 日期选择器 -->
                            <el-date-picker v-model="formInline.entrydate" type="daterange" range-separator="至" start-placeholder="开始日期"
                                end-placeholder="结束日期">
                            </el-date-picker>
                        </el-form-item>
                        <el-form-item>
                            <el-button type="primary" @click="onSubmit">查询</el-button>
                        </el-form-item>
                    </el-form>
                    <!-- 表格 -->
                    <el-table :data="tableData" border>
                        <el-table-column prop="name" label="姓名" width="180">
                        </el-table-column>
                        <el-table-column prop="image" label="图像" width="180">
                        </el-table-column>
                        <el-table-column prop="gender" label="性别" width="140">
                            <!-- <template slot-scope="scope">
                                {{ scope.row.gender == 1 ? '男': '女' }}
                            </template> -->
                        </el-table-column>
                        <el-table-column prop="job" label="职位" width="140">
                        </el-table-column>
                        <el-table-column prop="entrydate" label="入职日期" width="140">
                        </el-table-column>
                        <el-table-column prop="entrydate" label="入职日期" width="140">
                        </el-table-column>
                        <el-table-column label="操作">
                            <el-button type="primary" size="mini">编辑</el-button>
                            <el-button type="danger" size="mini">删除</el-button>
                        </el-table-column>
                    </el-table>
                </el-main>
            </el-container>
        </el-container>
    </div>
</template>

<script>
// import axios from 'axios';

export default {
    data() {
        return {
            tableData: [],
            formInline: {
                user: '',
                region: '',
                entrydate:[],
            }
        }
    },
    methods: {
        onSubmit() {
            alert('查询')
        }
    },
    // mounted() {
    //     //发送异步请求获取数据
    //     axios.get("").then((result) => {
    //         this.tableData = result.data.data;
    //     }).catch((err) => {
            
    //     });
    // },
}
</script>

<style></style>