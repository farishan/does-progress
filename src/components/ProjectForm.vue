<template>
	<div>
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
				</ul>

				<v-form v-model="valid">
					<v-layout>
						<v-flex md8>
					<v-slider
						v-model="project.progress"
						:max="100"
						:min="0"
						:step="1"
						label="Progress"
					></v-slider>
						</v-flex>
						<v-flex md4>
							<v-select
								class="pl-3"
								v-model="project.status"
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
								v-model="project.note"
								label="Note"
							></v-textarea>
						</v-flex>
						<v-flex class="ml-2">
							<v-textarea
								box
								v-model="project.problem"
								label="Problem"
							></v-textarea>
						</v-flex>
					</v-layout>

					<v-text-field
						v-model="project.name"
						:rules="rules"
						label="Project Name"
						required
						box
					></v-text-field>
					<v-layout class="my-3">
						<v-flex md6>
							<label>Start Date</label><br>
							<v-date-picker v-model="project.start" landscape></v-date-picker>
						</v-flex>
						<v-flex md6>
							<label>Deadline Date</label><br>
							<v-date-picker v-model="project.deadline" landscape></v-date-picker>
						</v-flex>
					</v-layout>

					<v-btn class="primary" @click="save">Submit</v-btn>
				</v-form>
			</v-card-text>
		</v-card>
					
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
				statusList: [
					'WIP',
					'WAPP',
					'LOCK'
				],

				valid: false,
				rules: [
					v => !!v || 'required'
				],

				project: {}
			}
		},
		mounted(){
			this.project = this.projectProps;
		},
		methods: {
			save(){
				this.$root.$emit('save-project', this.project);
				this.$root.$emit('go-to-dashboard', true);
			}
		},
		computed: {
			countdown(){
				// this.project.count = moment().to(this.project.deadline);
				return moment().to(this.project.deadline);
			}
		}
	}
</script>