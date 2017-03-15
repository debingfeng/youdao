<template>
    <div class="wrapper">
        <nav class="detail-nav title-font">
            <i class="icon icon-back" @click="back()"></i>
        </nav>

        <article class="note-container" >
            <h1 class="note-title" >{{ title }}</h1>
            <section class="note-detail">
                {{ content }}
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
				content: "笔记详情",
				updateUrl: "/index/index/update",
				detailUrl: "/index/index/detail"
			}
		},
		methods: {
			empty: function () {
				this.searchValue = '';
			},
			back: function () {
				this.$router.go(-1);
			},
			getDetail: function () {
				let that = this;
				let data = {
					title: that.title,
					content: that.content,
                    type: 1
                };

//				this.axios.post(that.detailUrl,{id:}).then((response) => {
//					console.log(response.data)
//				})

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
