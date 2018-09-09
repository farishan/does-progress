<template>
	<v-layout>

		<!-- Sidebar -->
		<v-flex md2>
			<AdminSidebar></AdminSidebar>
		</v-flex>
		
		<!-- Main content -->
		<v-flex md10>
			<v-container>
				<div v-if="page == 'dashboard'">
					<v-card>
						<v-card-title>
							<h2 class="mb-3">Project Info</h2>
						</v-card-title>
						<v-card-text>
							<!-- Preview -->
							<ul>
								<li>Project name: {{project.name}}</li>
								<li>Status: {{project.status}}</li>
								<li>Progress: {{project.progress}}</li>
								<li>Countdown: {{countdown}}</li>
								<li>Start: {{project.start}}</li>
								<li>Deadline: {{project.deadline}}</li>
								<li>Note: {{project.note}}</li>
								<li>Problem: {{project.problem}}</li>
								<li v-if="project.teams">Teams: {{project.teams.length}}</li>
							</ul>

							<v-btn class="primary" @click="page = 'project'">Edit Project</v-btn>
						</v-card-text>
					</v-card>

					<v-card>
						<v-card-title>This week team: {{project.selectedTeam}}</v-card-title>
						<v-card-text>
							<v-btn v-for="(team, i) in project.teams" @click="selectThisWeek(team)" :key="i">{{team.name}}</v-btn>
						</v-card-text>
					</v-card>
				</div>

				<!-- Project Form -->
				<div v-if="page == 'project'">
					<ProjectForm :projectProps="project"></ProjectForm>
				</div>

				<div v-if="page == 'team'">
					<TeamForm :projectProps="project"></TeamForm>
				</div>

				<div v-if="page == 'subteam'">
					<SubTeamForm :projectProps="project"></SubTeamForm>
				</div>
			</v-container>
		</v-flex>

	</v-layout>
</template>

<script>
	import moment from 'moment'
	import AdminSidebar from './AdminSidebar'
	import ProjectForm from './ProjectForm'
	import TeamForm from './TeamForm'
	import SubTeamForm from './SubTeamForm'

	export default {
		props: [
			'projectProps'
		],
		components: {
			AdminSidebar,
			ProjectForm,
			TeamForm,
			SubTeamForm
		},
		data: function(){
			return {
				page: 'dashboard',
				
				project: {}
			}
		},
		mounted(){
			var self = this;

			if(this.projectProps){
				this.project = this.projectProps;
			}

			this.$root.$on('route-change', function(route){
				self.page = route;
			});

			this.$root.$on('go-to-dashboard', function(res){
				if(res){
					self.page = 'dashboard'
				}
			});
		},
		methods: {
			selectThisWeek(team){
				this.project.selectedTeam = team;
				this.$root.$emit('save-project', this.project);

				this.$root.$emit('select-this-week-team', team);
			},
			
		},
		computed: {
			countdown(){
				// this.project.count = moment().to(this.project.deadline);
				return moment().to(this.project.deadline);
			}
		}
	}
</script>