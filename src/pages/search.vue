<template>
    <div class="wrapper">
        <nav class="search-nav title-font">
            <div class="search-box">

                <input type="search" class="search-input" v-model="searchValue" placeholder="搜索"> <i class="icon-close" @click="empty()" v-show="searchValue"></i>
                <span class="text-cancel" @click="back()">取消</span>
            </div>
            <div class="tip-box" v-show="searchValue" >
                您可能想找：
            </div>
        </nav>

        <div class="main-content" v-bind:class="[activeClass]">
            <div class="all" v-if="list.length > 0">
                <div class="yd-list" >
                    <section class="list-item" v-for="item in list">
                        <p class="item-theme">
                            <i :class="item.icon"></i>
                            <span class="item-title">{{item.title}}</span>
                        </p>
                        <p class="item-mark"><span class="item-time">{{item.date}}</span><span class="item-count">{{item.count}}</span></p>
                    </section>
                </div>
            </div>
        </div>
    </div>



</template>

<script>
	export default {
        components: {
        },
		data () {
			return {
				orderType: false,
				isActive: true,
				searchValue: "",
				activeClass: 'main-pos',
				list: [

				]
			}
		},
		methods: {
			tabFunc: function () {
				this.isActive = !this.isActive;
				this.orderType = !this.orderType;
			},
			empty: function () {
                this.searchValue = '';
			},
            back: function () {
				this.$router.go(-1);
			}
		},
		watch: {
			searchValue: function (val) {
				this.list.push({
					type: 3,
					title: val,
					date: "2017/01/01",
					count: ""
                })
			}

		},
		computed: {
			// a computed getter
			dataList: function () {
				// `this` points to the vm instance
				return this.list.filter(function(d){
					if (d.type == 1) {
						d.icon = "icon-note";
					} else if(d.type == 2){
						d.icon = "icon-md";
					} else {
						d.icon = "icon-folder";
					}
					return d.icon;
				});
			}
		},

	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .wrapper {
        width: 100%;
    }
    .main-pos {
        top: 35px;
    }
    /*头部导航*/
    .search-nav {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 60px;
        background-color: #398dee;
        z-index: 999;
    }
    .search-box {
        position: relative;
        top: 12px;
        width: 100%;
        height: 40px;
        padding: 0 15px;

    }
    .search-input {
        height: 36px;
        width: 85%;
        background-color: #f4f4f4;
        background-image: none;
        border: 1px solid #ccc;
        border-radius: 4px;
        -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075);
        box-shadow: inset 0 1px 1px rgba(0,0,0,.075);
    }
    .text-cancel {
        display: inline-block;
        padding: 5px;
        color: white;
    }
    .tip-box {
        position: absolute;
        top:60px;
        height: 35px;
        width: 100%;
        line-height: 35px;
        text-align: left;
        background-color: #fff6dd;
        padding: 0 15px;
    }
    input::-webkit-input-placeholder {
        text-align: center;
        font-size: 16px;
    }
    /*列表*/
    .yd-list {
        width: 100%;
    }
    .list-item {
        width: 100%;
        height: 75px;
        padding-top: 20px;
    }
    .item-theme {
        height: 22px;
        line-height: 22px;
    }
    .item-title {
        display: inline-block;
        font-size: 18px;
        text-indent: .5em;
        width: 80%;
        overflow: hidden;
        text-overflow:ellipsis;
        white-space: nowrap;
    }
    .icon-md {
        position: relative;
        top: -2px;
        display: inline-block;
        width: 18px;
        height: 18px;
        background: url("../assets/mdicon.png") no-repeat;
        background-size: 18px;
    }
    .icon-note {
        position: relative;
        top: -2px;
        display: inline-block;
        width: 18px;
        height: 18px;
        background: url("../assets/noteicon.png") no-repeat;
        background-size: 18px;
    }
    .icon-folder {
        position: relative;
        top: -3px;
        display: inline-block;
        width: 18px;
        height: 18px;
        background: url("../assets/folder.png") no-repeat;
        background-size: 18px;
    }
    .item-mark {
        margin-top: 15px;
        color: #c9c9c9;
    }
    .item-time {

    }
    .item-count {
        display: inline-block;
        margin-left: 20px;
    }

</style>
