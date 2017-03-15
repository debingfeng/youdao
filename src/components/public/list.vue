<template>
    <div class="yd-list">
        <section class="list-item" v-for="item in dataList">
            <p class="item-theme">
                <i :class="item.icon"></i>
                <span class="item-title">{{item.title}}</span>
            </p>
            <p class="item-mark"><span class="item-time">{{item.date}}</span><span class="item-count">{{item.count}}</span></p>
        </section>
    </div>
</template>

<script>
	export default {
		name: 'note',
        props: ['list'],
		data () {
			return {
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
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

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
        background: url("../../assets/mdicon.png") no-repeat;
        background-size: 18px;
    }
    .icon-note {
        position: relative;
        top: -2px;
        display: inline-block;
        width: 18px;
        height: 18px;
        background: url("../../assets/noteicon.png") no-repeat;
        background-size: 18px;
    }
    .icon-folder {
        position: relative;
        top: -3px;
        display: inline-block;
        width: 18px;
        height: 18px;
        background: url("../../assets/folder.png") no-repeat;
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
