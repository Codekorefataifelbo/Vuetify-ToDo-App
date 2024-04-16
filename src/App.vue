<template>
	<v-app>
        <v-navigation-drawer app :mobile-breakpoint="768" v-model="drawer">
            <v-img
                class="pa-4 pt-7"
				src="LandscapePic.png"
                height="170"
                
            >
                <v-avatar size="70" class="mb-2 border">
                    <img src="profile-pic.jpg" alt="user" />
                </v-avatar>
                <div style="color: white;" class="text-subtitle-1 font-weight-bold">
                    <a>Arif Ul Hoque</a>
                </div>
                <div style="color: white;" class="text-subtitle-2"><a href="https://www.linkedin.com/in/arif-hoque-83239189/">Software Engineer</a></div>
            </v-img>

			<v-list dense nav>
				<v-list-item v-for="item in items" :key="item.title" link :to="item.to">
					<v-list-item-icon>
						<v-icon>{{ item.icon }}</v-icon>
					</v-list-item-icon>

					<v-list-item-content>
						<v-list-item-title>{{ item.title }}</v-list-item-title>
					</v-list-item-content>
				</v-list-item>
			</v-list>
		</v-navigation-drawer>

		<v-app-bar
			app
			color="primary"
			dark
			src="LandscapePic.png"
			prominent
			:height="$route.path === '/' ? 236 : 170"
		>
			<template v-slot:img="{ props }">
				<v-img
					v-bind="props"
					
				></v-img>
			</template>

			<v-container class="header-container">
				<v-row>
					<v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
					<v-spacer></v-spacer>
					<search />
				</v-row>
				<v-row>
					<v-toolbar-title class="text-h4 ml-4">
						{{ $store.state.appTitle }}
					</v-toolbar-title>
				</v-row>
				<v-row>
					<live-date-time />
				</v-row>
				<v-row v-if="$route.path === '/'">
					<field-add-task />
				</v-row>
			</v-container>
		</v-app-bar>

		<v-main>
			<router-view></router-view>
			<snackbar />
		</v-main>
	</v-app>
</template>

<script>
export default {
	data: () => ({
		drawer: null,
		items: [
			{ title: 'Todo', icon: 'mdi-format-list-checks', to: '/' },
			{ title: 'About', icon: 'mdi-help-box', to: '/about' },
		],
	}),
	mounted() {
		this.$store.dispatch('getTasks')
	},
	components: {
		'field-add-task': require('@/components/Todo/FieldAddTask.vue').default,
		snackbar: require('@/components/Shared/Snackbar.vue').default,
		search: require('@/components/Tools/Search.vue').default,
		'live-date-time': require('@/components/Tools/LiveDateTime.vue').default,
	},
}
</script>

<style lang="scss">
.header-container {
	max-width: none !important;
}
</style>
