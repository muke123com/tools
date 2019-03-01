<template>
    <div class="page page-index">
        <div class="w-center">
            <div class="transform-box">
                <div class="tab">
                    <a href="javascript:void(0)" :class="{'active':t_type == 1}" :data-type="1" @click="selectType">Unicode编码</a>
                    <a href="javascript:void(0)" :class="{'active':t_type == 2}" :data-type="2" @click="selectType">Utf-8编码</a>
                    <a href="javascript:void(0)" :class="{'active':t_type == 3}" :data-type="3" @click="selectType">URL编码/解码</a>
                </div>
                <div class="content">
                    <div class="left box">
                        <textarea placeholder="" v-model="input_text"></textarea>
                    </div>
                    <div class="right box">
                        <textarea placeholder="转换后结果" v-model="output_text"></textarea>
                    </div>
                </div>
                <div class="btns">
                    <a href="javascript:void(0)" class="button" @click="wordToCoding">中文转编码</a>
                    <a href="javascript:void(0)" class="button" @click="codingToWord">编码转中文</a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Index',
        data() {
            return {
                t_type: 1, //转换类型
                input_text: '',
                output_text: ''
            }
        },
        methods: {
            selectType(e) {
                let type = e.currentTarget.dataset.type;
                this.t_type = type;
            },
            codingToWord(){
                switch (this.t_type){
                    case 1:
                        this.decodeUnicode();
                        break;
                    case 2:
                        break;
                    case 3:
                        break;
                }
            },
            wordToCoding(){
                switch (this.t_type){
                    case 1:
                        this.encodeUnicode();
                        break;
                    case 2:
                        break;
                    case 3:
                        break;
                }
            },
            encodeUnicode() {
                this.output_text = encodeUnicode(this.input_text);
            },
            decodeUnicode() {
                this.output_text = decodeUnicode(this.input_text);
            }

        }
    }

    // 转为unicode 编码
    function encodeUnicode(str) {
        let res = [];
        for (let i = 0; i < str.length; i++) {
            res[i] = ( "00" + str.charCodeAt(i).toString(16) ).slice(-4);
        }
        return "\\u" + res.join("\\u");
    }

    // 解码
    function decodeUnicode(str) {
        str = str.replace(/\\/g, "%");
        return unescape(str);
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    @import "index.css";
</style>
