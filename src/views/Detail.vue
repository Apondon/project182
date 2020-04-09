<template>
    <div>
        <el-row :gutter="20">
            <el-col :span="4">
                <!-- 图片区域 -->
                <div :class="cls" style='width:100%;height:150px;line-height:150px;text-align:center;font-size:60px;color:oranged'></div>
                <!-- 菜单 -->
                <div class="menu">
                    <p v-for='item in list' :key='item.id' :class="item.id == id?'active':''">{{item.name}}</p>
                </div>
            </el-col>
            <el-col :span="20">
                <!-- 上 -->
                <div class="up">
                    <h2 class="title">{{title}}</h2>
                    <p class="text">{{text}}</p>
                    <el-form :model="form">
                        <el-form-item label="书籍名称">
                            <el-radio-group v-model="form.book" @change="changeHandle">
                                <el-radio-button v-for='item in books' :key='item.id' :label="item.name"></el-radio-button>
                            </el-radio-group>
                        </el-form-item>
                        <el-form-item label="购买数量">
                            <el-input-number v-model="form.num" :min="0"></el-input-number>
                        </el-form-item>
                        <el-form-item label="适用校区">
                            <el-select v-model="form.school" placeholder="请选择">
                                <el-option  
                                v-for="item in schools" :key="item.value"
                                :label="item.label" :value="item.value">
                                </el-option>
                            </el-select>
                        </el-form-item>
                        <el-form-item label="总价">{{price}}</el-form-item>
                    </el-form>
                    <el-button type="primary" @click="clickHandle">立即购买</el-button>
                </div>
                <!-- 下 -->
                <div class="down">
                    <h2>书籍简介</h2>
                    <p>{{bookText}}</p>
                </div>
            </el-col>
        </el-row>
        <el-dialog :visible.sync="dialogTableVisible">
            <el-table :data="gridData" border>
                <el-table-column property="book" label="书籍名称" width="220"></el-table-column>
                <el-table-column property="num" label="购买数量" width="100"></el-table-column>
                <el-table-column property="school" label="适用校区" width="220"></el-table-column>
                <el-table-column property="price" label="单价"></el-table-column>
                <!-- 计算总价一 -->
                <el-table-column property="finalPrice" label="总价一"></el-table-column>
                <!-- 计算总价二 -->
                <el-table-column label="总价">
                    <template slot-scope="scope">
                        <span style="color:red">{{scope.row.num * scope.row.price}}</span>
                    </template>
                </el-table-column>
            </el-table>
            <el-button type="primary">立即购买</el-button>
        </el-dialog>
    </div>
</template>
<script>
export default {
    data(){
        return{
            id:'',
            cls:'',
            title:'111',//整套书标题
            text:'222',//整套书的简介
            bookText:'111', // 书籍简介
            books:[],
            // 整套书的表单
            form:{
                book:'',//选择购买的书名
                num:1,//购买数量
                school:'',//适用校区
                price:0, //书籍单价
            },

            // 数据
            list:[
                {
                    id:1,
                    name:'移动互联网开发书籍',
                    cls:'el-icon-s-help',
                    text:'直接通过设置类名为 el-icon-iconName 来使用即可',
                    books:[
                        {
                            id:'a1',
                            name:'book a1',
                            text:'这本书是book a1很有用',
                            price:30
                        },
                        {
                            id:'a2',
                            name:'book a2',
                            text:'这本书是book a2很有用',
                            price:35
                        },
                        {
                            id:'a3',
                            name:'book a3',
                            text:'这本书是book a3很有用',
                            price:40
                        }
                    ]
                },
                {
                    id:2,
                    name:'移动互联网应用书籍',
                    cls:'el-icon-mobile-phone',
                    text:'el-icon-iconName 来使用即可直接通过设置类名为',
                    books:[
                         {
                            id:'b1',
                            name:'book b1',
                            text:'这本书是book b1很有用',
                            price:30
                        },
                        {
                            id:'b2',
                            name:'book b2',
                            text:'这本书是book b2很有用',
                            price:35
                        },
                        {
                            id:'b3',
                            name:'book b3',
                            text:'这本书是book b3很有用',
                            price:40
                        }
                    ]
                },
                {
                    id:3,
                    name:'大数据书籍',
                    cls:'el-icon-upload',
                    text:'Button 组件提供除了默认值以外的三种尺寸，可以在不同场景下选择合适的按钮尺寸',
                    books:[
                         {
                            id:'c1',
                            name:'book c1',
                            text:'这本书是book c1很有用',
                            price:30
                        },
                        {
                            id:'c2',
                            name:'book c2',
                            text:'这本书是book c2很有用',
                            price:35
                        },
                        {
                            id:'c3',
                            name:'book c3',
                            text:'这本书是book c3很有用',
                            price:40
                        }
                    ]
                },
                {
                    id:4,
                    name:'人工智能书籍',
                    cls:'el-icon-s-opportunity',
                    text:'带图标的文字链接可增强辨识度',
                    books:[
                         {
                            id:'d1',
                            name:'book d1',
                            text:'这本书是book d1很有用',
                            price:30
                        },
                        {
                            id:'d2',
                            name:'book d2',
                            text:'这本书是book d2很有用',
                            price:35
                        },
                        {
                            id:'d3',
                            name:'book d3',
                            text:'这本书是book d3很有用',
                            price:40
                        }
                    ]
                }
            ],
            //学校数据
            schools: [{
                value: '北京大学',
                label: '北京大学'
                },
                {
                value: '清华大学',
                label: '清华大学'
                }, 
                {
                value: '人民大学',
                label: '人民大学'
                }, 
                {
                value: '北京理工',
                label: '北京理工'
                }, 
                {
                value: '中山大学',
                label: '中山大学'
            }],
            // 弹窗
            dialogTableVisible:false,
            gridData:[],
        }
    },
    computed:{
        price(){
            return this.form.num*this.form.price
        }
    },
    watch:{
        dialogTableVisible(newVal){
            if(!newVal) this.gridData = []
        }
    },
    mounted(){
        // 获取主页传来的id
        const id = this.$route.params.id
        this.id = id
        for(const item of this.list){
            if(id == item.id){
                this.cls = item.cls
                this.title = item.name
                this.text = item.text
                this.books = item.books
            }
        }
    },
    methods:{
        changeHandle(){
            for(const item of this.books){
                if(this.form.book == item.name){
                    this.form.price = item.price
                    this.bookText = item.text
                } 
            }
        },
        clickHandle(){
            this.dialogTableVisible = true
            this.form.finalPrice = this.form.num*this.form.price
            this.gridData.push(this.form)
        }
    }
}
</script>
<style lang="scss" scoped>
.el-col{
    background: #fff;
}
.menu{
    p{
        height: 30px;
        line-height: 30px;
    }
}
.active{
    background: cyan;
    color: #fff;
}
.text{
    height: 40px;
    line-height: 40px;
    background: rgb(247, 247, 142);
    color: grey;
    font-size: 14px;
    margin: 20px 0;
}
.el-radio-button{
    margin-right: 20px;;
}
</style>