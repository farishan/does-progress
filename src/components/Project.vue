<template>
	<v-layout>

		<!-- Sidebar -->
		<v-flex md2>
			<v-navigation-drawer permanent>
				<v-toolbar flat>
					<v-list>
						<v-list-tile>
							<v-list-tile-title class="title" @click="login">
							{{currentDate}}
							</v-list-tile-title>
						</v-list-tile>
					</v-list>
				</v-toolbar>

				<v-divider></v-divider>
				
				<!-- Project time range -->
				<div class="pa-3">
					Start: {{project.start}} <br>
					Deadline: {{project.deadline}}
				</div>
				
				<!-- Project info -->
				<div class="pa-3">
					<ul>
						<li>Project: "{{project.name}}"</li>
						<li>Status: {{project.status}}</li>
						<li>Progress: {{project.progress}}</li>
						<li>Countdown: {{project.countdown}}</li>
						<li>Note: {{project.note}}</li>
						<li>Problem: {{project.problem}}</li>
					</ul>
				</div>
				
				<!-- Time Schedule -->
				<div class="pa-3">
					<h3>Time Schedule</h3>
					<ul>
						<li v-for="(team, i) in project.teams" :key="i">{{team.name}}
							<ul>
								<li>Time: {{team.start}} - {{team.deadline}}</li>
								<li>Countdown: {{team.countdown}}</li>
							</ul>
						</li>
					</ul>
				</div>

			</v-navigation-drawer>
		</v-flex>

		<!-- Main Content -->
		<v-flex md10 v-if="project.selectedTeam">
			<div class="header pa-3">
				<h1>{{title}} | <small>This week: {{project.selectedTeam.name}} <span class="grey--text">({{project.selectedTeam.spv}})</span></small></h1>
			</div>
			<v-container>
				
				<!-- Note, Problem, Info -->
				<v-layout>
					<v-flex md5>
						<v-card>
							<v-card-title>Note</v-card-title>
							<v-card-text>
								{{project.selectedTeam.note}}
							</v-card-text>
						</v-card>
					</v-flex>
					<v-flex md5>
						<v-card>
							<v-card-title>Problem</v-card-title>
							<v-card-text>
								{{project.selectedTeam.problem}}
							</v-card-text>
						</v-card>
					</v-flex>

					<!-- Team info -->
					<v-flex md2>
						<v-card>
							<v-card-text>
								<ul>
									<li>Status: {{project.selectedTeam.status}}</li>
									<li>Progress: {{project.selectedTeam.progress}}</li>
									<li>Countdown: {{project.selectedTeam.countdown}}</li>
								</ul>
							</v-card-text>
						</v-card>
					</v-flex>
				</v-layout>
				
				<v-divider class="my-3"></v-divider>

				<!-- Subs -->
				<template v-for="(sub, i) in project.selectedTeam.subs">
					<v-card class="mb-1" :key="i">
						<v-card-title>{{sub.name}}</v-card-title>
						<v-card-text>
							<!-- Info -->
							<v-layout>
								<v-flex md5>
									<p><b>Note</b>: {{sub.note}}</p>
								</v-flex>
								<v-flex md5>
									<p><b>Problem</b>: {{sub.problem}}</p>
								</v-flex>
								<v-flex md2>
									<ul>
										<li>Status: {{sub.status}}</li>
										<li>Progress: {{sub.progress}}%</li>
										<li>Countdown: {{sub.countdown}}</li>
									</ul>
								</v-flex>
							</v-layout>
						</v-card-text>
					</v-card>
				</template>

			</v-container>
		</v-flex>
	</v-layout>
</template>

<script>
	import moment from 'moment';
	export default {
		props: [
			'projectProps'
		],
		data: function(){
			return {
				title: 'Die Hard Fans',
				author: 'Does University',
				currentDate: '',

				project: {}
			}
		},
		mounted: function(){
			this.currentDate = moment().format('DD MMM YYYY');
			this.project = this.projectProps;
		},
		methods: {
			login(){
				this.$root.$emit('login', true);
			}
		}
	}
</script>