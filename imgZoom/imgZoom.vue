<template>
    <div>
        <div v-for="(item, index) in imgList" :key="index" class="img-zoom">
            <span class="img-preview" @click="handlePictureCardPreview(picViewUrl + item.relativeUrl)">
                <i class="el-icon-zoom-in"></i>
            </span>
            <el-image style="width: 100px;height:100px" :src="picViewUrl + item.relativeUrl">
            </el-image>
        </div>
        <el-dialog :visible.sync="dialogVisible">
            <el-image style="width:100%" :src="dialogImageUrl">
            </el-image>
        </el-dialog>
    </div>
</template>

<script>
    import { mapState } from "vuex";
    export default {
        name: 'imgZoom',
        props: {
            imgList: { type: Array, default: () => [] }, // 图片路径Arry
        },
        computed: mapState(["picViewUrl"]),
        data() {
            return {
                dialogImageUrl: '',
                dialogVisible: false,
            }
        },
        methods: {
            handlePictureCardPreview(file) {
                this.dialogImageUrl = file;
                this.dialogVisible = true;
            }
        }
    }
</script>
<style scoped>
    .img-zoom {
        position: relative;
        display: inline-block;
        width: 100px;
        height: 100px;
        margin-right: 10px;
    }

    .img-zoom .img-preview {
        position: absolute;
        width: 100%;
        height: 100%;
        left: 0;
        top: 0;
        cursor: pointer;
        text-align: center;
        color: #fff;
        opacity: 0.9;
        font-size: 20px;
        background-color: rgba(0, 0, 0, 0.5);
        transition: opacity .3s;
        z-index: 1;
        display: none;
    }

    .img-zoom .img-preview .el-icon-zoom-in {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        opacity: 1;
    }

    .img-zoom:hover .img-preview {
        display: block !important;
    }
</style>