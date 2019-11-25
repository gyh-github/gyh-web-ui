<template>
    <div class="modalDiv" ref="modal">
        <div class="mainDiv" ref="main">
            <div class="topDiv">
                <strong>标题</strong>
            </div>
            <div class="contentDiv">
                <p>这是自己封装的模态框</p>
            </div>
            <div class="bottomDiv">
                <button @click="cancelFun">取消</button>
                <button>确认</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "modal",
        data(){
            return{

            }
        },
        props:['width'],
        methods:{
            //取消模态框
            cancelFun(){
                this.$emit('cancel')
            }
        },
        mounted(){
            const _this = this;
            let _cWidth = document.body.clientWidth - 0;
            let _width = _this.width || 400;
            let _left = (_cWidth - _width) / 2;
            _this.$nextTick(() => {
                _this.$refs.main.style.width = _width +'px';
                _this.$refs.main.style.left = _left +'px';
                _this.$refs.main.style.top = 100 +'px';
            })
            window.onresize = () => {
                _cWidth = document.body.clientWidth - 0;
                _left = (_cWidth - _width) / 2;
                _this.$nextTick(() => {
                    _this.$refs.main.style.width = _width +'px';
                    _this.$refs.main.style.left = _left +'px';
                    _this.$refs.main.style.top = 100 +'px';
                })
            }
        }
    }
</script>

<style type="text/scss" lang="scss" scoped>
    .modalDiv{
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        background: rgba(0, 0, 0, 0.4 );
        z-index: 1000;
        div.mainDiv{
            position: absolute;
            top: 0;
            background: #ffffff;
            transition-duration: 0.3s;
            border-radius: 5px;
            overflow: hidden;
            font-size: 0;
            div.topDiv{
                text-align: center;
                line-height: 50px;
                border-bottom: thin solid #dcdcdc;
                font-size: 20px;
            }
            div.contentDiv{
                text-align: center;
                line-height: 30px;
                font-size: 16px;
            }
            div.bottomDiv{
                text-align: center;
                button{
                    width: 50%;
                    line-height: 40px;
                    font-size: 16px;
                    &:nth-child(1){
                        background: #eeeeee;
                    }
                    &:nth-child(2){
                        background: #2ab219;
                        color: #ffffff;
                    }
                }
            }
        }
    }
</style>
