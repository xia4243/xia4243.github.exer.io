<template>
    <div id="app1">
        <!-- button按钮 -->
        <el-row>
            <el-button>默认按钮</el-button>
            <el-button type="primary">主要按钮</el-button>
            <el-button type="success">成功按钮</el-button>
            <el-button type="info">信息按钮</el-button>
            <el-button type="warning">警告按钮</el-button>
            <el-button type="danger">危险按钮</el-button>
        </el-row>
        <br>

        <!-- <el-row>
            <el-button plain>朴素按钮</el-button>
            <el-button type="primary" plain>主要按钮</el-button>
            <el-button type="success" plain>成功按钮</el-button>
            <el-button type="info" plain>信息按钮</el-button>
            <el-button type="warning" plain>警告按钮</el-button>
            <el-button type="danger" plain>危险按钮</el-button>
        </el-row>

        <el-row>
            <el-button round>圆角按钮</el-button>
            <el-button type="primary" round>主要按钮</el-button>
            <el-button type="success" round>成功按钮</el-button>
            <el-button type="info" round>信息按钮</el-button>
            <el-button type="warning" round>警告按钮</el-button>
            <el-button type="danger" round>危险按钮</el-button>
        </el-row>

        <el-row>
            <el-button icon="el-icon-search" circle></el-button>
            <el-button type="primary" icon="el-icon-edit" circle></el-button>
            <el-button type="success" icon="el-icon-check" circle></el-button>
            <el-button type="info" icon="el-icon-message" circle></el-button>
            <el-button type="warning" icon="el-icon-star-off" circle></el-button>
            <el-button type="danger" icon="el-icon-delete" circle></el-button>
        </el-row> -->

        <!-- table表格 -->
        <el-table :data="tableData" border style="width: 100%">
            <el-table-column prop="date" label="日期" width="180"></el-table-column>
            <el-table-column prop="name" label="姓名" width="180"></el-table-column>
            <el-table-column prop="address" label="地址"></el-table-column>
        </el-table>
        <!-- 分页 -->
        <el-pagination background layout="sizes, prev, pager, next" @size-change="handleSizeChange"
            @current-change="handleCurrentChange" :total="1000">
        </el-pagination>
        <br>
        <!-- 文件上传 -->
        <el-upload class="upload-demo" action="https://jsonplaceholder.typicode.com/posts/" :on-preview="handlePreview"
            :on-remove="handleRemove" :before-remove="beforeRemove" multiple :limit="3" :on-exceed="handleExceed"
            :file-list="fileList">
            <el-button size="small" type="primary">点击上传</el-button>
            <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
        </el-upload>
        <br>
        <!-- 好吃的汉堡 -->
        <el-row>
            <el-col :span="8" v-for="(o, index) in 2" :key="o" :offset="index > 0 ? 2 : 0">
                <el-card :body-style="{ padding: '0px' }">
                    <img src="https://ts1.cn.mm.bing.net/th/id/R-C.fb5ffd611901657bad91b685d3284cb7?rik=DkZ2ToQwmhdvkA&riu=http%3a%2f%2fwww.mingxing.com%2fUpload%2fArticles%2f1%2f0%2f538%2f538824_20210403101058335.jpg&ehk=1PS2H6XuZDP3nn93v7a4cv5Zb49cP0d4JzNjFDJE5hA%3d&risl=&pid=ImgRaw&r=0"
                        class="image">
                    <div style="padding: 14px;">
                        <span>好吃的汉堡</span>
                        <div class="bottom clearfix">
                            <time class="time">{{ currentDate }}</time>
                            <el-button type="text" class="button" @click="gen">操作按钮</el-button>
                        </div>
                    </div>
                </el-card>
            </el-col>
        </el-row>
        <br>
        <!-- 对话框 -->
        <!-- Table -->
        <el-button type="text" @click="dialogTableVisible = true">打开嵌套表格的 Dialog</el-button>

        <el-dialog title="收货地址" :visible.sync="dialogTableVisible">
            <el-table :data="gridData">
                <el-table-column property="date" label="日期" width="150"></el-table-column>
                <el-table-column property="name" label="姓名" width="200"></el-table-column>
                <el-table-column property="address" label="地址"></el-table-column>
            </el-table>
        </el-dialog>
        <br>
        <!-- 对话框展示From表单 -->
        <el-button type="text" @click="dialogFromVisible = true">from表单</el-button>

        <el-dialog title="from表单" :visible.sync="dialogFromVisible">
            <el-form ref="form" :model="form" label-width="80px">
                <el-form-item label="活动名称">
                    <el-input v-model="form.name"></el-input>
                </el-form-item>
                <el-form-item label="活动区域">
                    <el-select v-model="form.region" placeholder="请选择活动区域">
                        <el-option label="区域一" value="shanghai"></el-option>
                        <el-option label="区域二" value="beijing"></el-option>
                    </el-select>
                </el-form-item>
                <el-form-item label="活动时间">
                    <el-col :span="11">
                        <el-date-picker type="date" placeholder="选择日期" v-model="form.date1"
                            style="width: 100%;"></el-date-picker>
                    </el-col>
                    <el-col class="line" :span="2">-</el-col>
                    <el-col :span="11">
                        <el-time-picker placeholder="选择时间" v-model="form.date2" style="width: 100%;"></el-time-picker>
                    </el-col>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" @click="onSubmit">立即创建</el-button>
                    <el-button>取消</el-button>
                </el-form-item>
            </el-form>
        </el-dialog>
        <br>
        <el-container>
            <el-aside width="200px">
                <el-menu :default-openeds="['1', '3']">
                    <el-submenu index="1" >
                        <template slot="title"><i class="el-icon-message"></i>系统信息管理</template>

                        <el-menu-item index="1-1" >
                            <router-link to="/emp" text-decoration: none>员工管理</router-link>
                        </el-menu-item>

                        <el-menu-item index="1-2">
                            <router-link to="/element">部门管理</router-link>
                        </el-menu-item>

                    </el-submenu>

                </el-menu>
            </el-aside>
        </el-container>



    </div>
</template>

<script>

export default {

    data() {
        return {
            form: {
                name: '',
                region: '',
                date1: '',
                date2: '',
            },
            tableData: [{
                date: '2016-05-02',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1518 弄'
            }, {
                date: '2016-05-04',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1517 弄'
            }, {
                date: '2016-05-01',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1519 弄'
            }, {
                date: '2016-05-03',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1516 弄'
            }],
            fileList: [{
                name: 'food.jpeg',
                url: 'https://cn.bing.com/images/search?view=detailV2&ccid=%2b1%2f9YRkB&id=30E76007B8601555C062906F179A30844E76460E&thid=OIP.-1_9YRkBZXutkbaF0yhMtwHaEd&mediaurl=https%3a%2f%2fts1.cn.mm.bing.net%2fth%2fid%2fR-C.fb5ffd611901657bad91b685d3284cb7%3frik%3dDkZ2ToQwmhdvkA%26riu%3dhttp%253a%252f%252fwww.mingxing.com%252fUpload%252fArticles%252f1%252f0%252f538%252f538824_20210403101058335.jpg%26ehk%3d1PS2H6XuZDP3nn93v7a4cv5Zb49cP0d4JzNjFDJE5hA%253d%26risl%3d%26pid%3dImgRaw%26r%3d0&exph=415&expw=690&q=%e5%ad%99%e7%ac%91%e5%b7%9d&simid=608055902397281037&FORM=IRPRST&ck=F0F97BD758A68AE11FBC49BCE75AA899&selectedIndex=1'
            }, {
                name: 'food2.jpeg',
                url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100'
            }],
            currentDate: new Date(),
            gridData: [{
                date: '2016-05-02',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1518 弄'
            }, {
                date: '2016-05-04',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1518 弄'
            }, {
                date: '2016-05-01',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1518 弄'
            }, {
                date: '2016-05-03',
                name: '王小虎',
                address: '上海市普陀区金沙江路 1518 弄'
            }],
            dialogTableVisible: false,
            dialogFromVisible: false,
        }
    },
    methods: {
        handleSizeChange: function (val) {
            alert(val)
        },
        handleCurrentChange: function (val) {
            alert(val)
        },
        handleChange(file, fileList) {
            this.fileList = fileList.slice(-3);
        },
        gen() {
            alert('hhh')
        },
        onSubmit() {
            alert(this.form),
                this.dialogFromVisible = false
        }

    }
}
</script>
<style>
#app2{
    text-decoration: none;
}
.time {
    font-size: 13px;
    color: #999;
}

.bottom {
    margin-top: 13px;
    line-height: 12px;
}

.button {
    padding: 0;
    float: right;
}

.image {
    width: 100%;
    display: block;
}

.clearfix:before,
.clearfix:after {
    display: table;
    content: "";
}

.clearfix:after {
    clear: both
}
</style>
