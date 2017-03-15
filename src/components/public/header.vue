<template>
    <nav class="fix-nav title-font">
        <div class="avatar-box">
            <img src="../../assets/avatar.jpg" class="avatar" alt="">
        </div>
        <span class="current-type type-box" v-bind:class="{ active: isActive }" @click="tabFunc()">最新</span>
        <span class="current-type type-box" v-bind:class="{ active: !isActive }" @click="tabFunc()">全部</span>
    </nav>
</template>

<script>
	export default {
		name: 'header',
		props: ['type'],
        data (){
			return {
				isActive: true
            }
        },
        methods: {
			tabFunc: function () {
				this.isActive = !this.isActive;
			}
        }
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .fix-nav {
        position: fixed;
        top: 0;
        left: 0;
        /*居中显示*/
        /*left: 50%;*/
        /*max-width: 640px;*/
        /*min-width: 320px;*/
        /*transform: translateX(-50%);*/

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

</style>
