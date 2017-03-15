<template>
    <div>
        <v-header></v-header>
        <div class="main-content">
            <h1>profile</h1>
            <i class="icon icon-add"></i>
            <i class="icon icon-enter"></i>
            <i class="icon icon-folder"></i>
            <i class="icon icon-group"></i>
            <i class="icon icon-group-active"></i>
            <i class="icon icon-ic_survey"></i>
            <i class="icon icon-ic_synchronous"></i>
            <i class="icon icon-order"></i>
            <i class="icon icon-note-active"></i>
            <i class="icon icon-note"></i>
            <i class="icon icon-profile"></i>
            <i class="icon icon-profile-active"></i>
            <i class="icon icon-survey"></i>
        </div>
        <v-footer></v-footer>
    </div>



</template>

<script>
	import header from "../components/public/header.vue";
	import footer from "../components/public/footer.vue";
	import all from "../components/index/folder-list.vue";
	import list from "../components/public/list.vue";
	export default {
		components: {
			"v-header": header,
			"v-footer": footer,
			"v-folder": all,
			"v-list": list
		},
		data () {
			return {
			}
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
