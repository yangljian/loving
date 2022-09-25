<template>
    <div id="app">
        <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
        <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
        <div id="box" style="text-align: center;">
            <transition name="mybox">
                <img class="box" v-show="boxshow" src="./assets/达菲家族.jpeg"></img>
            </transition>
        </div>
        <el-button :style="display" type="primary" @click="togglebox">隐藏彩蛋</el-button>
    </div>
</template>
<script>
import StyleEditor from './components/StyleEditor'
import ResumeEditor from './components/ResumeEditor'
import './assets/reset.css'
let isPc = (function () {
    var userAgentInfo = navigator.userAgent;
    var Agents = ["Android", "iPhone",
        "SymbianOS", "Windows Phone",
        "iPad", "iPod"
    ];
    var flag = true;
    for (var v = 0; v < Agents.length; v++) {
        if (userAgentInfo.indexOf(Agents[v]) > 0) {
            flag = false;
            break;
        }
    }
    return flag;
}());
let getDateDiff = function (startDate, endDate) {
    var startTime = new Date(Date.parse(startDate.replace(/-/g, "/"))).getTime();
    var endTime = new Date(Date.parse(endDate.replace(/-/g, "/"))).getTime();
    var dates = Math.abs((startTime - endTime)) / (1000 * 60 * 60 * 24);
    return dates;
}
document.title += getDateDiff((new Date()).getFullYear() + '-' + ((new Date()).getMonth() + 1) + '-' + (new Date()).getDate(), '2022-05-31') + 1 + '天';
export default {
    name: 'app',
    components: {
        StyleEditor,
        ResumeEditor
    },
    data() {
        return {
            interval: 0.1,
            display: "display:none",
            boxshow: false,
            currentStyle: '',
            enableHtml: false,
            fullStyle: [
                `/*
* Hi。瑄宝！
* 这么久了。还没好好和你说过我的工作呢！
* 我是个后端工程师，俗称程序员。但是，总所周知，后端工程师是比较枯燥的，还好我会点前端技术，也就是网页相关的 ~~^-^~~。
* 接下来我会以前端的角度来开启此次奇妙之旅～
* 如这个页面。就是个什么也没有的网页。
* 现在我给这些空白的页面加点儿东西。
* 嗯。说起来手机和电脑还得区分一下。
* 你现在用的是。。。${isPc ? '电脑' : '手机'}
*/

/* 首先给所有元素加上过渡效果 */
* {
  -webkit-transition: all .3s;
  transition: all .3s;
}
/* 白色背景太单调了。来点背景 */
html, body, #app {
    display: block;
    height: 100%;
    background: url(/static/img/迪斯尼.bd971a9.jpeg);
    background-size: cover;
}
/* 文字太近了 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  ${isPc ? 'width: 48%;height: 96%;' : 'width: 96%;height: 50%;'}
  font-size: 14px;
  line-height:1.5;
}
/* 这些代码颜色都一样。加点儿高亮区别来 */
.token.selector{ color: rgb(133,153,0) }
.token.property{ color: rgb(187,137,0) }
.token.punctuation{ color: yellow }
.token.function{ color: rgb(42,161,152) }
.token.comment{ color: rgb(177,177,177) }
/* 加个 3D 效果 */
html{
  -webkit-perspective: 1000px;
          perspective: 1000px;
}
.styleEditor {
  position: fixed; 
  ${isPc ? 'left: 0;' : 'left:0;right:0;margin:auto;'}
  top: 0; 
  -webkit-transition: none; 
  transition: none;   
  ${isPc ? '-webkit-transform: rotateY(10deg) translateZ(-100px) ;transform: rotateY(10deg) translateZ(-100px) ;' : '-webkit-transform: rotateX(-10deg) translateZ(-100px) ;transform: rotateX(-10deg) translateZ(-100px) ;'}
  ${isPc ? '' : '-webkit-transform-origin: 50% 0% 0;transform-origin: 50% 0% 0;'}
}

/* 再来一张信纸 */
.resumeEditor{
  position: fixed; 
  ${isPc ? 'right: 0;' : 'left:0;right:0;margin:auto;'}
  ${isPc ? 'top: 0;' : 'bottom:2%;'}
  padding: .5em;  
  ${isPc ? 'margin: .5em;' : ''}
  ${isPc ? 'width: 48%;height: 96%;' : 'width: 96%;height: 50%;'}
  border: 1px solid;
  color: #222;
  overflow: auto;
  font-size: 14px;
  line-height:1.5;
  ${isPc ? '-webkit-transform: rotateY(-10deg) translateZ(-100px) ;transform: rotateY(-10deg) translateZ(-100px) ;' : '-webkit-transform: rotateX(10deg) translateZ(-100px) ;transform: rotateX(10deg) translateZ(-100px) ;'}
    ${isPc ? '' : '-webkit-transform-origin: 50% 0% 0;transform-origin: 50% 0% 0;'}
  }
/* 我开始写了 */


`,
                `
/* 是不是看着很简陋粗糙？
 * 因为这是 Markdown 格式的
 * 一种程序员用来写文档日志的简易语言
 * 翻译成 网页 就行了
 */
`,
                `
/* 再加点样式 */
.resumeEditor{
  padding: 2em;
  line-height:1.8;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
  font-size:18px;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;            
  content: counters(section, ".") " ";  
  margin-right: .5em;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: rgba(221,221,221,.5);
}

/* OK。完成！ */
...
/* 等会，再给宝加个彩蛋～～～ */
`
            ],
            currentMarkdown: '',
            fullMarkdown: `yang & xuan
----
2022年04月16日，走进了彼此世界，无话不谈。
2022年05月03日，初初见面，两人齐齐心动。  
2022年05月31日，我们在一起了。
已有 \`${getDateDiff((new Date()).getFullYear() + '-' + ((new Date()).getMonth() + 1) + '-' + (new Date()).getDate(), '2022-05-31') + 1}\` 天

一起吃过的餐厅
----

=====烤肉=====
* 明洞王妃家
* Day by Day
* 肉本家

=====杭帮菜=====
* 绿茶餐厅
* 新白鹿
* 弄堂里
* 新榆园
* 新发现
* 南京大牌档

=====东北菜=====
* 厨创
* 于掌勺

=====粤菜=====
* 点都德
* 蝴蝶里
* 避风塘
* 澳门味道茶餐
* 六顺福记茶楼

=====火锅=====
* 海底捞

=====面馆=====
* 和府捞面

=====创意菜=====
* 宴遇

=====墨西哥菜=====
* 梵美里

=====日料=====
* 浅草屋

=====韩料=====
* 听说过

=====新加坡菜=====
* 星洲小馆

=====意大利餐厅=====
* 菲滋意式餐厅

一起看过的电影
----

* 哆啦A梦
* 侏罗纪公园
* 遇见你
* 独行月球
* 杨戬
* 人生大事
* 霸道总裁和我的365天

一起玩过的剧本杀
----

* 雪乡连环杀人事件（卓司元&李开心）
* 月下沙利叶（肖律凡&乔雨）
* 权倾天下（刘宏&大乔）
* 漓川怪谈簿（星野笃静&良子）
* 拆迁（张论文&宋美容）

一起玩过的游戏
----

* 分手厨房
* 双人成行
* 放风筝
* 夹娃娃
* 财富流沙盘

一起参加的运动
----

* 射箭
* 羽毛球

一起看过的脱口秀
----

* 会说笑
* 松果脱口秀
* 魔脱

> 【Screw the world!!!I have my dear Xuanxuan】  
> 嘿，我不只想影响你的习惯。我还要去改变你的人生！
`
        }
    },
    created() {
        this.makeResume()
    },

    methods: {
        togglebox: function () {
            this.boxshow = !this.boxshow;
        },
        click() {
            alert(123);
        },
        makeResume: async function () {
            await this.progressivelyShowStyle(0)
            await this.progressivelyShowResume()
            await this.progressivelyShowStyle(1)
            await this.showHtml()
            await this.progressivelyShowStyle(2)
            this.display = "display:block;position: absolute;bottom: 0px;background-color: #FF00FF;border-color: #FF00FF;"
        },
        showHtml: function () {
            return new Promise((resolve, reject) => {
                this.enableHtml = true
                resolve()
            })
        },
        progressivelyShowStyle(n) {
            return new Promise((resolve, reject) => {
                let interval = this.interval
                let showStyle = (async function () {
                    let style = this.fullStyle[n]
                    if (!style) {
                        return
                    }
                    // 计算前 n 个 style 的字符总数
                    let length = this.fullStyle.filter((_, index) => index <= n).map((item) => item.length).reduce((p, c) => p + c, 0)
                    let prefixLength = length - style.length
                    if (this.currentStyle.length < length) {
                        let l = this.currentStyle.length - prefixLength
                        let char = style.substring(l, l + 1) || ' '
                        this.currentStyle += char
                        if (style.substring(l - 1, l) === '\n' && this.$refs.styleEditor) {
                            this.$nextTick(() => {
                                this.$refs.styleEditor.goBottom()
                            })
                        }
                        setTimeout(showStyle, interval)
                    } else {
                        resolve()
                    }
                }).bind(this)
                showStyle()
            })
        },
        progressivelyShowResume() {
            return new Promise((resolve, reject) => {
                let length = this.fullMarkdown.length
                let interval = this.interval
                let showResume = () => {
                    if (this.currentMarkdown.length < length) {
                        this.currentMarkdown = this.fullMarkdown.substring(0, this.currentMarkdown.length + 1)
                        let lastChar = this.currentMarkdown[this.currentMarkdown.length - 1]
                        let prevChar = this.currentMarkdown[this.currentMarkdown.length - 2]
                        if (prevChar === '\n' && this.$refs.resumeEditor) {
                            this.$nextTick(() => this.$refs.resumeEditor.goBottom())
                        }
                        setTimeout(showResume, interval)
                    } else {
                        resolve()
                    }
                }
                showResume()
            })
        }
    }
}
</script>
<style scoped>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

html {
    min-height: 100%;
}

.styleEditor {
    -webkit-backface-visibility: hidden;
}

.box {
    position: relative;
}

//给过渡的name加样式

.mybox-enter-active {
    transiton: all 2s ease
}

.mybox-enter {

    opacity: 0;
}

.mybox-leave {
    transiton: all 2s ease
}

.mybox-leave-active {

    opacity: 0;
}
</style>
