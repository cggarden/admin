<template>
    <el-row :gutter="20">
        <el-col :span="8"><div class="grid-content bg-purple"><p style="width:100px;float:left;color: #ccc;">代表姓名</p><p style="width:100px;float: left">张小明</p></div></el-col>
        <el-col :span="8"><div class="grid-content bg-purple"><p style="width:100px;float:left;color: #ccc;">代表团</p><p style="width:100px;float: left">西安市代表团</p></div></el-col>
        <el-col :span="8"><div class="grid-content bg-purple"><p style="width:100px;float:left;color: #ccc;">代表证号</p><p style="width:100px;float: left">6101111980xxxx0057</p></div></el-col>
        <el-col :span="8"><div class="grid-content bg-purple"><p style="width:100px;float:left;color: #ccc;">邮政编号</p><p style="width:100px;float: left">710000</p></div></el-col>
        <el-col :span="8"><div class="grid-content bg-purple"><p style="width:100px;float:left;color: #ccc;">联系电话</p><p style="width:100px;float: left">6101111980xxxx0057</p></div></el-col>
        <el-col :span="8"><div class="grid-content bg-purple"><p style="width:100px;float:left;color: #ccc;">通讯地址</p><p style="width:100px;float: left">陕西省西安市</p></div></el-col>
        <el-col :span="3"><div class="grid-content bg-purple"><i style="float:left;padding:20px 0px;color:red;">*</i>
            <p style="float:left;height:30px;line-height:30px;margin-left: 10px;color:#ccc;">建议类别</p></div> </el-col>
        <el-col :span="21"><div class="grid-content bg-purple"style="float:left;padding:10px 0px;"> <el-select v-model="value4" clearable placeholder="城市建设">
            <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value"></el-option>
        </el-select></div> </el-col>
        <el-col style="clear: both"></el-col>
        <el-col :span="3"><div class="grid-content bg-purple"><i style="float:left;padding:20px 0px;color:red;">*</i>
            <p style="float:left;height:30px;line-height:30px;margin-left: 10px;color:#ccc;">建议标题</p></div> </el-col>
        <el-col :span="21"><div class="grid-content bg-purple"style="float:left;padding:14px 0px;">
            <input style="height:24px;width: 460px;" placeholder="请输入标题"/></div> </el-col>
        <el-col :span="3"><div class="grid-content bg-purple"><i style="float:left;padding:20px 0px;color:red;">*</i>
            <p style="float:left;height:30px;line-height:30px;margin-left: 10px;color:#ccc;">建议内容</p></div> </el-col>
        <el-col :span="21"><div class="grid-content bg-purple"style="float:left;padding:14px 0px;"></div>
            <button @click="getUEContent()">获取内容</button>
            <div class="editor-container">
                <UE :defaultMsg=defaultMsg :config=config :id=ue1 ref="ue"></UE>
            </div>
        </el-col>
        <el-col :span="3"><div class="grid-content bg-purple">
            <p style="float:left;height:30px;line-height:30px;margin-left: 10px;color:#ccc;text-align: right;">附件</p></div> </el-col>
        <el-col :span="21"><div class="grid-content bg-purple"style="float:left;padding:10px 0px;">
            <el-upload
                    class="upload-demo"
                    action="https://jsonplaceholder.typicode.com/posts/"
                    :on-preview="handlePreview"
                    :on-remove="handleRemove"
                    multiple
                    :limit="3"
                    :on-exceed="handleExceed"
                    :file-list="fileList">
                <el-button size="small" type="primary">点击上传</el-button>
                <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
            </el-upload>
        </div> </el-col>
        <el-col :span="3"><div class="grid-content bg-purple">
            <p style="float:left;height:30px;line-height:30px;margin-left: 10px;color:#ccc;">审查意见</p></div> </el-col>
        <el-col :span="21"><div class="grid-content bg-purple"style="float:left;padding:18px 0px;">
            <el-radio v-model="radio" label="1">立案</el-radio>
            <el-radio v-model="radio" label="2">不予立案</el-radio>
            <el-radio v-model="radio" label="3">参文件</el-radio>
        </div> </el-col>
        <el-col style="clear: both"></el-col>
        <el-col :span="3"><div class="grid-content bg-purple">
            <p style="float:left;height:30px;line-height:30px;margin-left: 10px;color:#ccc;">办理方式</p></div> </el-col>
        <el-col :span="21"><div class="grid-content bg-purple"style="float:left;padding:18px 0px;">
            <el-radio v-model="radio2" label="1">主办/会办</el-radio>
            <el-radio v-model="radio2" label="2">分办</el-radio>
        </div> </el-col>
        <el-col style="clear: both"></el-col>
        <el-col :span="3"><div class="grid-content bg-purple">
            <p style="float:left;height:30px;line-height:30px;margin-left: 10px;color:#ccc;">办理单位</p></div> </el-col>
        <el-col :span="21"><div class="grid-content bg-purple"style="float:left;padding:12px 0px;">
            <el-form :inline="true" :model="formInline" class="demo-form-inline">
                <el-form-item>
                    <el-select v-model="formInline.region" placeholder="活动区域" style="width:300px;">
                        <el-option label="区域一" value="shanghai"></el-option>
                        <el-option label="区域二" value="beijing"></el-option>
                    </el-select>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" plain @click="onSubmit">选择主办单位</el-button>
                </el-form-item>
            </el-form>
        </div> </el-col>
        <el-col :span="3"><div class="grid-content bg-purple">
            <p style="float:left;height:30px;line-height:30px;margin-left: 10px;color:#ccc;"></p></div> </el-col>
        <el-col :span="21"><div class="grid-content bg-purple"style="float:left;padding:12px 0px;">
            <el-form :inline="true" :model="formInline" class="demo-form-inline">
                <el-form-item>
                    <el-select v-model="formInline.region" placeholder="活动区域" style="width:300px;">
                        <el-option label="区域一" value="shanghai"></el-option>
                        <el-option label="区域二" value="beijing"></el-option>
                    </el-select>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" plain @click="onSubmit">选择会办单位</el-button>
                </el-form-item>
            </el-form>
        </div> </el-col>
        <el-col :span="3"><div class="grid-content bg-purple">
            <p style="float:left;height:30px;line-height:30px;margin-left: 10px;color:#ccc;">建议联系人</p></div> </el-col>
        <el-col :span="21"><div class="grid-content bg-purple"style="float:left;padding:12px 0px;">
            <el-select v-model="value5" ref="value5" @change="change"  multiple placeholder="请选择" style="width:300px;">
                <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value"></el-option>
            </el-select>
        </div><el-button type="primary" plain style="margin:12px 12px;width:64px;float: left;">选择</el-button>
            <p style="float:left;height:30px;line-height:30px;margin-left: 10px;color:#ccc;">已选:{{2}}人</p> </el-col>
        <el-col :span="3"><div class="grid-content bg-purple">
            <p style="float:left;height:30px;line-height:30px;margin-left: 10px;color:#ccc;">建议附议人</p></div> </el-col>
        <el-col :span="21"><div class="grid-content bg-purple"style="float:left;padding:12px 0px;">
            <el-select v-model="value5" ref="value5" @change="change"  multiple placeholder="请选择" style="width:300px;">
                <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value"></el-option>
            </el-select>
        </div><el-button type="primary" plain style="margin:12px 12px;width:64px;float: left;">选择</el-button>
            <p style="float:left;height:30px;line-height:30px;margin-left: 10px;color:#ccc;">已选:{{2}}人</p> </el-col>
        <el-col :span="3"><div class="grid-content bg-purple">
            <p style="float:left;height:30px;line-height:30px;margin-left: 10px;color:#ccc;"></p></div> </el-col>
        <el-col :span="2"><el-button type="primary">提交建议</el-button></el-col>
        <el-col :span="2"><el-button type="primary">存为草稿</el-button></el-col>
        <el-col :span="2"><el-button type="primary" plain>重置</el-button></el-col>
        <el-col :span="2"><el-button type="primary" plain>取消</el-button></el-col>
    </el-row>

</template>
<script>
    import UE from '../../components/ue/ue.vue';
    import ElButton from "../../../node_modules/element-ui/packages/button/src/button.vue";
    export default {
        components: {
            ElButton,
            UE},
        data() {
            return {
                options: [{
                    value: '选项1',
                    label: '民生'
                }, {
                    value: '选项2',
                    label: '家乐'
                },],
                number:2,
                formInline: {
                    region: ''
                },
                fileList: [{name: 'food.jpeg', url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100'},
                    {name: 'food2.jpeg', url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100'}],

                defaultMsg: '这里是UE测试',
                config: {
                    initialFrameWidth: null,
                    initialFrameHeight: 200
                },
                ue1: "ue1", // 不同编辑器必须不同的id
                radio: '1',
                radio2: '1',
                value4:[],
                value5: [],
            }
        },
        methods: {
            handleRemove(file, fileList) {
                console.log(file, fileList);
            },
            handlePreview(file) {
                console.log(file);
            },
            handleExceed(files, fileList) {
                this.$message.warning(`当前限制选择 3 个文件，本次选择了 ${files.length} 个文件，共选择了 ${files.length + fileList.length} 个文件`);
            },
            change:function(){
                console.log(value5.value)
            },
            getUEContent() {
                let content = this.$refs.ue.getUEContent(); // 调用子组件方法
                this.$notify({
                    title: '获取成功，可在控制台查看！',
                    message: content,
                    type: 'success'
                });
                console.log(content)
            },
            onSubmit() {
                console.log('submit!');
            },
        }
    }
</script>
<style>
    .base_news{
        list-style-type: none;
        width:100%;
        display: flex;
    }
    .info{
        border-radius: 10px;
        line-height: 20px;
        padding: 10px;
        margin: 10px;
        background-color: #ffffff;
    }
</style>