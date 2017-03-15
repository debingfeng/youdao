<template>
    <div class="wrapper">
        <nav class="detail-nav title-font">
            <i class="icon icon-back" @click="back()"></i>
        </nav>

        <article class="note-container" >
            <h1 class="note-title" >{{ title }}</h1>
            <section class="note-detail">
                {{ detail }}
                <article class="markdown-body"><h2 id="方案一-基于vuejs-2x系列-element-ui内容管理系统解决方案" data-source-line="1"><a class="markdownIt-Anchor" href="#方案一-基于vuejs-2x系列-element-ui内容管理系统解决方案"></a>方案一 基于Vue.js 2.x系列 + element-ui内容管理系统解决方案</h2>
                    <ul data-source-line="5">
                        <li>
                            <p>Vue.js 2.x系列 参考地址：<a href="http://cn.vuejs.org/v2/guide/">http://cn.vuejs.org/v2/guide/</a></p>
                        </li>
                        <li>
                            <p>element-ui     参考地址：<a href="http://element.eleme.io/#/zh-CN/component/installation">http://element.eleme.io/#/zh-CN/component/installation</a></p>
                        </li>
                    </ul>
                    <p data-source-line="10"><strong>整理文档内容应该包括</strong></p>
                    <p data-source-line="12">效果演示图可以参考：<a href="https://liyu365.github.io/BG-UI/tpl/#page/desktop.html">https://liyu365.github.io/BG-UI/tpl/#page/desktop.html</a></p>
                    <p data-source-line="14">前言</p>
                    <p data-source-line="16">这个解决方案适合什么场景，为什么采用这个解决方案，有什么有点与缺点，后续扩展与维护，自己想说点什么就说什么。</p>
                    <p data-source-line="18">1、目录结构介绍</p>
                    <p data-source-line="20">2、安装步骤</p>
                    <p data-source-line="22">3、组件使用说明与演示</p>
                    <p data-source-line="24">4、调试部署上传</p>
                    <p data-source-line="26">5、单元测试（可选）</p>
                    <p data-source-line="28">6、其他注意事项</p>
                    <h3 id="表格" data-source-line="31"><a class="markdownIt-Anchor" href="#表格"></a>表格</h3>
                    <ul data-source-line="33">
                        <li>
                            <p>基础表格</p>
                        </li>
                        <li>
                            <p>Datatable</p>
                            <p>参考 <a href="http://datatables.club/">Datatable中文网</a></p>
                        </li>
                    </ul>
                    <h3 id="表单" data-source-line="39"><a class="markdownIt-Anchor" href="#表单"></a>表单</h3>
                    <ul data-source-line="41">
                        <li>
                            <p>基本表单</p>
                        </li>
                        <li>
                            <p>编辑器</p>
                            <p>可以参考富文本编辑器markdow支持组件
                                Laverna  <a href="https://laverna.cc/index.html">https://laverna.cc/index.html</a></p>
                        </li>
                        <li>
                            <p>文件上传</p>
                            <p>上传组件使用webuploader
                                <a href="http://fex.baidu.com/webuploader/getting-started.html">http://fex.baidu.com/webuploader/getting-started.html</a></p>
                        </li>
                        <li>
                            <p>图片裁剪</p>
                        </li>
                        <li>
                            <p>日期控件</p>
                        </li>
                    </ul>
                    <h3 id="ui元素" data-source-line="56"><a class="markdownIt-Anchor" href="#ui元素"></a>UI元素</h3>
                    <ul data-source-line="58">
                        <li>弹出框alert</li>
                        <li>确认框confirm</li>
                        <li>提示框</li>
                        <li>树形图</li>
                    </ul>
                    <h2 id="方案二-jquery-bootstrap" data-source-line="67"><a class="markdownIt-Anchor" href="#方案二-jquery-bootstrap"></a>方案二 jquery + bootstrap</h2>
                    <p data-source-line="69">目录结构及快速构建</p>
                    <p data-source-line="71">参考现有方案： H-ui,amazeui,BG-ui</p>
                    <h2 id="方案三-angular2-ui-bootstrap" data-source-line="74"><a class="markdownIt-Anchor" href="#方案三-angular2-ui-bootstrap"></a>方案三 angular2 + ui-bootstrap</h2>
                </article>
            </section>
        </article>
        <footer class="detail-option">
            <div class="flex-item">
                <section class="btn">编辑</section>
            </div>
            <div class="flex-item">
                <section class="btn">删除</section>
            </div>
            <div class="flex-item">
                <section class="btn">移动</section>
            </div>
        </footer>
    </div>


</template>

<script>
	export default {
		components: {},
		data () {
			return {
				title: "笔记标题",
                detail: "笔记详情"
			}
		},
		methods: {
			empty: function () {
				this.searchValue = '';
			},
			back: function () {
				this.$router.go(-1);
			}
		},

	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .wrapper {
        width: 100%;
    }

    /*头部导航*/
    .detail-nav {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 60px;
        background-color: #398dee;
        z-index: 999;
    }


    .icon-back {
        position: relative;
        top: 15px;
        left: 15px;
        background: url("../assets/back.png") no-repeat;
        background-size: 32px;
    }
    .note-container {
        position: relative;
        padding: 60px 15px;
        z-index: 1;
    }
    .note-title {
        position: relative;
        padding: 10px 0;
    }
    .note-title:after {
        content:"";
        position: absolute;
        bottom: 0;
        left: 0;
        right: 0;
        border-bottom: 1px solid #e7e7e7;
        -webkit-transform:scaleY(.5);
        -webkit-transform-origin:0 0;
    }
    .note-detail {
        padding: 10px 0;
    }
    .detail-option {
        position: fixed;
        bottom: 0;
        left: 0;
        display: flex;
        align-items: center;
        width: 100%;
        height: 60px;
        border-top: 1px #cacaca solid;
        background-color: ghostwhite;
        z-index: 999;
    }
    .flex-item {
        display: flex;
        flex: 1;
        justify-content: center;
    }
    .btn {
        width: 50px;
        height: 50px;
        line-height: 50px;
        border-radius: 25px;
        text-align: center;
        color: white;
        background-color: #5e97d8;
    }
</style>
