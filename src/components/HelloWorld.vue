<template>
    <div>
        <div class="edit">
            <div id="canvas1">
                <canvas id="canvas" width="600" height="600"></canvas>
            </div>
            <div id="editUtils">
                <i class="el-icon-share" @click="openImg"></i>
                <i class="el-icon-edit" @click="choosePen"></i>
                <i class="el-icon-zoom-in" @click="zoomIn"></i>
                <i class="el-icon-zoom-out" @click="zoomOut"></i>
                <i class="el-icon-download" @click="download"></i>
                <i class="el-icon-check" @click="send"></i>
            </div>
        </div>
    </div>
</template>

<script>
    import  {fabric} from 'fabric'
    export default {
        name: 'HelloWorld',
        props: {
            msg: String
        },
        data(){
            return{
                canvas:{},
            }
        },
        methods:{
            openImg(){
                // create a rectangle object
                /*var rect = new  fabric.Rect({
                    left: 100,
                    top: 100,
                    fill: 'red',
                    width: 20,
                    height: 20
                });*/

                fabric.Object.prototype.transparentCorners = false;
                fabric.Object.prototype.cornerColor = 'blue';
                fabric.Object.prototype.cornerStyle = 'circle';

                var rect = new fabric.Rect({
                    left: 100,
                    top: 50,
                    fill: '',
                    width: 200,
                    height: 100,
                    objectCaching: false,
                    stroke: 'cyan',
                    strokeWidth: 4,
                });

                rect.on('selected', function() {//选中监听事件
                    console.log('selected a rectangle');
                });

                this.canvas.add(rect);
                this.canvas.setActiveObject(rect);
                console.log("打开图片")
                this.canvas.isDrawingMode = false;

            },
            choosePen(){
                /*var rect = new fabric.Rect({
                    left: 20,
                    top: 20,
                    fill: '#F2f2f2',
                    width: 20,
                    height: 20,
                    angle: 45
                });*/
                var circle = new fabric.Circle({ radius: 75, fill: 'yellow' });
                this.canvas.add(circle);
                console.log("选择画笔")
                this.canvas.isDrawingMode = false;
            },
            zoomIn(){
                var line = new fabric.Line([10, 10, 100, 100], {
                    fill: 'green',
                    stroke: 'green',    //笔触颜色
                    strokeWidth: 2,//笔触宽度
                });
                this.canvas.add(line);
                this.canvas.isDrawingMode = true;
                this.canvas.freeDrawingBrush.color = "#E34F51"
                console.log("zoomIn")
            },
            zoomOut(){
                this.canvas.setBackgroundImage('https://img.tupianzj.com/uploads/200408/9-20040Q05K2H5.jpg', this.canvas.renderAll.bind(this.canvas));
                this.__canvases.push(this.canvas);
                console.log("zoomOut")
            },
            download(){
                console.log("下载图片")
            },
            send(){
                console.log(this.canvas.toJSON())
                console.log("确定并发送")
            }
        },
        mounted() {
            this.canvas = new fabric.Canvas('canvas');
            console.log("mounted.........")
        },
        created() {
            console.log("created is igitited...")
        },
        beforeDestroy() {
            console.log("beforeDestory .....")
        }
    }
</script>

<style scoped>
    * {
        padding: 0;
        margin: 0;
    }

    .edit {
        display: flex;
        flex-direction: column;
        justify-items: center;
        justify-content: center;
    }

    #editUtils {
        display: flex;
        height: 30px;
        width: 600px;
        background-color: #f2f2f2;
        margin: 0 auto;
        color: gray;
        flex-direction: row;
        justify-items: center;
        justify-content: space-evenly;
        line-height: 48px;
        text-align: center;
        font-size: 24px;
    }

    #canvas1 {
        display: flex;
        justify-content: center;
        margin: 10px auto;
        width: 600px;
        height: 600px;
        /*background-color: whitesmoke;*/
    }
</style>
