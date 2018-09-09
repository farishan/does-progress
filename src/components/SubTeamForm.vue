<template>
	<div>

		<!-- Add new sub team form -->
		<div v-if="isAdding">
			<h2 class="mb-3">Add New Sub-Team</h2>

			<!-- Preview -->
			<ul>
				<li>Sub Team Name: {{inputedTeam.name}}</li>
				<li>Parent Team: {{inputedTeam.parent}}</li>
				<li>Status: {{inputedTeam.status}}</li>
				<li>Progress: {{inputedTeam.progress}}</li>
				<li>Countdown: {{countdown}}</li>
				<li>Start: {{inputedTeam.start}}</li>
				<li>Deadline: {{inputedTeam.deadline}}</li>
				<li>Note: {{inputedTeam.note}}</li>
				<li>Problem: {{inputedTeam.problem}}</li>
			</ul>

			<v-form v-model="valid">
				<v-layout>
					<v-flex md8>
						<v-slider
							v-model="inputedTeam.progress"
							:max="100"
							:min="0"
							:step="1"
							label="Progress"
						></v-slider>
					</v-flex>
					<v-flex md4>
						<v-select
							class="pl-3"
							v-model="inputedTeam.status"
							:items="statusList"
							label="Status"
							box
						></v-select>
					</v-flex>
				</v-layout>

				<v-layout>
					<v-flex class="mr-2">
						<v-textarea
							box
								v-model="inputedTeam.note"
								label="Note"
							></v-textarea>
					</v-flex>
					<v-flex class="ml-2">
						<v-textarea
							box
							v-model="inputedTeam.problem"
							label="Problem"
						></v-textarea>
					</v-flex>
				</v-layout>

				<v-layout>
					<v-flex>
						<v-text-field
							v-model="inputedTeam.name"
							:rules="rules"
							label="inputedTeam Name"
							required
							box
						></v-text-field>
					</v-flex>
					<v-flex>
						<v-select
							class="pl-3"
							v-model="inputedTeam.parent"
							:items="teams"
							label="Parent"
							box
						></v-select>
					</v-flex>
				</v-layout>

				<v-layout class="my-3">
					<v-flex md6>
						<label>Start Date</label><br>
						<v-date-picker v-model="inputedTeam.start" landscape></v-date-picker>
					</v-flex>
					<v-flex md6>
						<label>Deadline Date</label><br>
						<v-date-picker v-model="inputedTeam.deadline" landscape></v-date-picker>
					</v-flex>
				</v-layout>

				<v-btn @click="isAdding = false">Cancel</v-btn>
				<v-btn class="primary" @click="save">Submit</v-btn>
			</v-form>
		</div>

		<div v-else>
			<v-toolbar flat color="white">
				<v-toolbar-title>Sub Team</v-toolbar-title>
				<v-divider
					class="mx-2"
					inset
					vertical
				></v-divider>
				<v-spacer></v-spacer>
				<v-btn color="primary" dark class="mb-2" @click="isAdding = true">New Sub Team</v-btn>
			</v-toolbar>
			
			<v-card>
				<v-card-title>Select team</v-card-title>
				<v-card-text>
					<v-layout>
						<v-flex v-for="(team, i) in project.teams" :key="i">
							<v-btn :key="i" @click="selectedTeam = team">{{team.name}}</v-btn>
						</v-flex>
					</v-layout>
				</v-card-text>
			</v-card>

			<v-card v-if="selectedTeam" class="mt-3">
				<v-card-title>
					<h3>{{selectedTeam.name}}</h3>
				</v-card-title>
				<v-card-text>
					<p v-if="selectedTeam.subs.length == 0">
						No subs.
					</p>
					<div v-else>
						<table>
							<thead>
								<tr>
									<td>Name</td>
									<td>Progress</td>
									<td>Status</td>
									<td>Note</td>
									<td>Problem</td>
									<td>Action</td>
								</tr>
							</thead>
							<tbody>
								<template v-for="(team, i) in selectedTeam.subs">
									<tr :key="i">
										<td>{{team.name}}</td>
										<td>{{team.progress}}</td>
										<td>{{team.status}}</td>
										<td>{{team.note}}</td>
										<td>{{team.problem}}</td>
										<td>
											<v-btn @click="edit(team, i)">edit</v-btn>
											<v-btn @click="deleteItem(team, i)">delete</v-btn>
										</td>
									</tr>
								</template>
							</tbody>
						</table>
					</div>
				</v-card-text>
			</v-card>

		</div>
	</div>
</template>

<script>
	import moment from 'moment'
	export default {
		props: [
		'projectProps'
		],
		data: function(){
			return {
				isAdding: false,

				statusList: [
					'WIP',
					'WAPP',
					'LOCK'
				],

				valid: false,
				rules: [
					v => !!v || 'required'
				],

				inputedTeam: {},

				project: {},

				teams: [],
				selectedTeam: null,
				editIndex: -1
			}
		},
		mounted () {
			this.project = this.projectProps;

			if(this.project.teams){
				for (var i = 0; i < this.project.teams.length; i++) {
					this.teams.push(this.project.teams[i].name)
				}
			}
		},
		methods: {
			edit(team, i){
				this.inputedTeam = team;
				this.isAdding = true;
				this.editIndex = i;
			},
			deleteItem(team, index){
				for (var i = 0; i < this.project.teams.length; i++) {
					if(this.project.teams[i].name == team.parent){
						this.project.teams[i].subs.splice(index, 1);
					}
				}
				this.$root.$emit('save-project', this.project);
			},
			save(){
				for (var i = 0; i < this.project.teams.length; i++) {
					if(this.project.teams[i].name == this.inputedTeam.parent){
						if(this.editIndex > -1){
							this.project.teams[i].subs[this.editIndex] = this.inputedTeam;
						}else{
							this.project.teams[i].subs.push(this.inputedTeam)
						}
					}
				}
				this.$root.$emit('save-project', this.project);
				this.isAdding = false;
				this.editIndex = -1;
			}
		},
		computed: {
			countdown(){
				// this.project.count = moment().to(this.project.deadline);
				return moment().to(this.inputedTeam.deadline);
			}
		}

	}
</script>

<style scoped>
	table {
		width: 100%;
	}
	table td {
		border: 1px solid #ddd;
		padding: .25rem .5rem;
	}
	table thead td {
		background-color: #eee;
		font-weight: 700;
	}
</style>