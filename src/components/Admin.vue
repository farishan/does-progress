<template>
	<v-layout>

		<!-- Sidebar -->
		<v-flex md2>
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
						@click=""
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
		</v-flex>
		
		<!-- Main content -->
		<v-flex md10>
			<v-container>
				<!-- Project Section -->
				<div>
					<h2 class="mb-3">Project Info</h2>
					{{project}}
					{{countdown}}
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
									v-model="project.status"
				          :items="statusList"
				          label="Status"
				        ></v-select>
							</v-flex>
						</v-layout>

		        <v-layout>
		        	<v-flex class="mr-2">
				        <v-textarea
									v-model="project.note"
									label="Note"
								></v-textarea>
		        	</v-flex>
		        	<v-flex class="ml-2">
								<v-textarea
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
						></v-text-field>
						<v-layout class="my-3">
							<v-flex md6>
								<label>Start Date</label><br>
								<v-date-picker v-model="project.start" landscape></v-date-picker>
							</v-flex>
							<v-flex md6>
								<label>Deadline Date</label><br>
								<v-date-picker v-model="project.end" landscape></v-date-picker>
							</v-flex>
						</v-layout>
					</v-form>
				</div>
			</v-container>
		</v-flex>

	</v-layout>
</template>

<script>
	import moment from 'moment'
	export default {
		data: function(){
			return {
				items: [
					{ title: 'Dashboard', icon: 'dashboard' },
          { title: 'Project', icon: 'dashboard' },
          { title: 'Team', icon: 'question_answer' }
        ],
        right: null,

        statusList: [
        	'WIP',
        	'WAPP',
        	'LOCK'
        ],

				valid: false,
				rules: [
					v => !!v || 'required'
				],

				project: {
					name: '',
					start: null,
					deadline: null,
					note: '',
					problem: '',
					status: '',
					progress: 0,
					count: 0
				}
			}
		},
		mounted(){
			
		},
		computed: {
			countdown(){
				return moment().to(this.project.end);
			}
		}
	}
</script>