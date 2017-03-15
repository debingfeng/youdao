<template>
    <div class="wrapper">
        <nav class="fix-nav title-font">
            <div class="avatar-box">
                <img src="../assets/avatar.jpg" class="avatar" alt="">
            </div>
            <span class="current-type type-box" v-bind:class="{ active: isActive }" @click="setLatest()" >最新</span>
            <span class="current-type type-box" v-bind:class="{ active: !isActive }" @click="setAll()" >全部</span>
        </nav>
        <div class="main-content">

            <div class="latest-box" v-show="isActive">
                <input type="text" class="search-input" @click="openView('/search')" placeholder="搜索">
            </div>

            <div class="search-box" v-show="!isActive">
                <i class="icon icon-add-folder folder-pos"></i>
                <input type="text" class="search-input" @click="openView('/search')" placeholder="搜索">
                <i class="icon icon-order order-pos"></i>
            </div>

            <div class="yd-list">

                <section class="list-item" @click="openView('/detail',item.id,item.type)" v-for="item in dataList">
                    <p class="item-theme">
                        <i :class="item.icon"></i>
                        {{item.type}}
                        <span class="item-title">{{item.title}}</span>
                    </p>
                    <p class="item-mark"><span class="item-time">{{item.modify_time|test}}</span><span class="item-count">{{item.count}}</span>
                    </p>
                </section>
                <infinite-loading :on-infinite="onInfinite" ref="infiniteLoading" spinner="spiral" >
                    <span slot="no-more">
                      <h3>没有更多了</h3>
                    </span>
                </infinite-loading>
            </div>
        </div>
        <v-footer></v-footer>
        <div class="fix-add">
            <i class="icon icon-add" ></i>
        </div>

    </div>

</template>

<script>
	import footer from "../components/public/footer.vue";
	import InfiniteLoading from 'vue-infinite-loading';
	export default {
		components: {
			"v-footer": footer,
			InfiniteLoading
		},
		data () {
			return {
				orderType: true,
				isActive: true,
				tab: "latest",
                index: "index",
                url: '/youdao/index/latest',
                page: 1,
                pageSize: 5,
                pageTotal: 0,
                findItem: '/youdao/index/findItem',
				list: [],

			}
		},
		methods: {
			onInfinite() {
				let that = this;
                that.axios.get(that.url,{params: { page:that.page,pagesize:that.pageSize }}).then((response) => {
                    let result = response.data;
                    that.pageTotal = result.data.pageTotal;
                    if (that.page >= that.pageTotal) {
                        that.$refs.infiniteLoading.$emit('$InfiniteLoading:complete');
                        return false;
                    }
                    that.page++;
                    that.list = that.list.concat(result.data.list);
                    that.$refs.infiniteLoading.$emit('$InfiniteLoading:loaded');
                });
			},
			changeFilter() {
				this.list = [];
				this.$nextTick(() => {
					this.$refs.infiniteLoading.$emit('$InfiniteLoading:reset');
				});
			},
            setLatest: function () {
				if (this.isActive) return;
                this.isActive = true;
                this.url = '/youdao/index/latest';
				this.page = 1;
				this.changeFilter();
			},
            setAll: function () {
				if (!this.isActive) return;
				this.page = 1;
				this.isActive = false;
				this.url = '/youdao/index/index';
				this.changeFilter();
			},
			openView: function (url,id,type) {
				let that = this;
				if (type != 3) {
					return that.$router.push({path: url});
                }
				that.axios.post(this.findItem,{id:id}).then((response) => {
					console.log(response.data);
					that.list = response.data;
				})

			},
            getAllData: function () {
				let that = this;
				let timer = setTimeout(() => {
					that.isActive = true;
					that.axios.get(that.latestUrl).then((response) => {
						let result = response.data;
						that.pageTotal = result.data.pageTotal;
						if (that.page >= that.pageTotal) {
							that.$refs.infiniteLoading.$emit('$InfiniteLoading:complete');
							return false;
						}
						that.page++;
						that.list = that.list.concat(result.data.list);
						that.$refs.infiniteLoading.$emit('$InfiniteLoading:loaded');
						clearTimeout(timer);
					});
				}, 1000);
			}
		},
		created: function () {
//			let that = this;
//			that.axios.post('/index/index/test',{name:"name",age:"age"}).then((response) => {
//				console.log(response.data);
//				that.list = response.data;
//			})
		},
		mounted: function () {
//			this.getLatestData();
		},
		computed: {
			// a computed getter
			dataList: function () {
				// `this` points to the vm instance
				return this.list.filter(function (d) {
					if (d.type == 1) {
						d.icon = "icon-note";
					} else if (d.type == 2) {
						d.icon = "icon-md";
					} else {
						d.icon = "icon-folder";
					}
					return d.icon;
				});
			}
		},
		filters: {
			test: function (t) {

                return new Date(parseInt(t) * 1000).toLocaleString().replace(/:\d{1,2}$/,' ');
			}
        }

	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .wrapper {
        width: 100%;
    }
    .fix-add {
        position: fixed;
        bottom: 75px;
        right: 30px;
        display: flex;
        align-items: center;
        justify-content: center;
        width: 50px;
        height: 50px;
        border-radius: 25px;
        background-color: #1bcc5a;
    }

    /*头部导航*/
    .fix-nav {
        position: fixed;
        top: 0;
        left: 0;

        width: 100%;
        height: 60px;
        line-height: 60px;
        text-align: center;
        background-color: #398dee;
        z-index: 999;
    }

    .avatar-box {
        position: absolute;
        top: 14px;
        left: 14px;
    }

    .avatar {
        display: inline-block;
        width: 32px;
        height: 32px;
        border-radius: 16px;
    }

    .type-box {
        color: white;
        padding: 5px;
        opacity: .6;
    }

    .active {
        opacity: 1;
        border-bottom: 1px solid;
    }

    /*tab切换*/
    .search-box {
        position: relative;
        width: 100%;
        height: 45px;
        line-height: 45px;
        padding: 10px 45px;
        /*background-color: gray;*/
    }

    .latest-box {
        position: relative;
        width: 100%;
        height: 45px;
        line-height: 45px;
        padding: 10px 0;
    }

    .search-input {
        width: 100%;
        height: 38px;
        text-indent: 0.5em;
        background-color: #f4f4f4;
        background-image: none;
        border: 1px solid #ccc;
        border-radius: 4px;
        -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075);
        box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075);
    }

    .folder-pos {
        position: absolute;
        left: 0;
        top: 17px;
    }

    .order-pos {
        position: absolute;
        right: 0;
        top: 17px;
    }

    input::-webkit-input-placeholder {
        text-align: center;
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
        text-overflow: ellipsis;
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
