<template>
	<v-app>
		<!-- {{project.selectedTeam}} -->
		<template v-if="project.name">
			<Admin :projectProps="project" v-if="showAdmin"></Admin>
			<Project :projectProps="project" v-if="!showAdmin"></Project>
		</template>
	</v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Project from './components/Project'
import Admin from './components/Admin'

export default {
	name: 'App',
	components: {
		HelloWorld,
		Project,
		Admin
	},
	mounted () {
		var self = this;

		if(localStorage.getItem('does-progress-project-data')){
			this.project = JSON.parse(localStorage.getItem('does-progress-project-data'));
		}else{
			this.project = {
				count: 0,
				deadline: '2018-09-27',
				name: 'Default Project',
				note: 'note',
				problem: 'problem',
				progress: 23,
				start: '2018-09-11',
				status: 'WIP',
				teams: [],
				selectedTeam: {}
			}
		}

		this.$root.$on('select-this-week-team', function(res){
			self.project.selectedTeam = res;
		})

		this.$root.$on('save-project', function(project){
			self.save(project);
		});

		this.$root.$on('login', function(){
			self.showAdmin = true;
		});

		this.$root.$on('logout', function(){
			self.showAdmin = false;
		});

		// console.log('APP.VUE project:' , this.project)
	},
	data () {
		return {
			showAdmin: true,
			project: {}
		}
	},
	methods: {
		save(project){
			self.project = project;

			var data = JSON.stringify(project);
			localStorage.setItem('does-progress-project-data', data);
		}
	}
}
</script>
