<template>
	<v-navigation-drawer permanent>
		<v-toolbar flat>
			<v-list>
				<v-list-tile>
					<v-list-tile-title class="title">
						Admin
					</v-list-tile-title>
				</v-list-tile>
			</v-list>
		</v-toolbar>

		<v-divider></v-divider>
		<v-list dense class="pt-0">
			<v-list-tile
				v-for="item in items"
				:key="item.title"
				@click="goto(item.route)"
			>
				<v-list-tile-action>
					<v-icon>{{ item.icon }}</v-icon>
				</v-list-tile-action>

				<v-list-tile-content>
					<v-list-tile-title>{{ item.title }}</v-list-tile-title>
				</v-list-tile-content>
			</v-list-tile>
		</v-list>
	</v-navigation-drawer>
</template>

<script>
	export default {
		data: function(){
			return {
				items: [
					{ title: 'Dashboard', icon: 'dashboard', route: 'dashboard' },
					{ title: 'Project', icon: 'dashboard', route: 'project' },
					{ title: 'Team', icon: 'question_answer', route: 'team' },
					{ title: 'Team - Sub', icon: 'question_answer', route: 'subteam' },
					{ title: 'Logout', icon: 'question_answer', route: 'logout' }
				],
				right: null
			}
		},
		mounted(){
			
		},
		methods: {
			goto(val){
				if(val == 'logout'){
					this.$root.$emit('logout', true);
				}else{
					this.$root.$emit('route-change', val);
				}
			}
		}
	}
</script>