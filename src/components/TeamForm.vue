<template>
	<div>
		<v-toolbar flat color="white">
			<v-toolbar-title>Team</v-toolbar-title>
			<v-divider
				class="mx-2"
				inset
				vertical
			></v-divider>
			<v-spacer></v-spacer>
			<v-dialog v-model="dialog" max-width="800px">
				<v-btn slot="activator" color="primary" dark class="mb-2">New Team</v-btn>
				<v-card>
					<v-card-title>
						<span class="headline">{{ formTitle }}</span>
					</v-card-title>

					<v-card-text>
						<v-container grid-list-md>
							<v-layout wrap>
								<v-flex xs12 sm6 md6>
									<v-text-field v-model="editedItem.name" label="Name"></v-text-field>
								</v-flex>
								<v-flex xs12 sm6 md6>
									<v-text-field v-model="editedItem.spv" label="Supervisor"></v-text-field>
								</v-flex>
								<v-flex xs12 sm6 md6>
									<v-select
										v-model="editedItem.status"
										:items="statusList"
										label="Status"
									></v-select>
								</v-flex>
								<v-flex xs12 sm6 md6>
									<v-text-field v-model="editedItem.progress" label="Progress"></v-text-field>
								</v-flex>

								<v-flex xs12 sm6 md6>
									<v-textarea v-model="editedItem.note" label="Note"></v-textarea>
								</v-flex>
								<v-flex xs12 sm6 md6>
									<v-textarea v-model="editedItem.problem" label="Problem"></v-textarea>
								</v-flex>

								<v-flex xs12 sm6 md6>
									<p>Start</p>
									<v-date-picker v-model="editedItem.start"></v-date-picker>
								</v-flex>
								<v-flex xs12 sm6 md6>
									<p>Deadline</p>
									<v-date-picker v-model="editedItem.deadline"></v-date-picker>
								</v-flex>
							</v-layout>
						</v-container>
					</v-card-text>

					<v-card-actions>
						<v-spacer></v-spacer>
						<v-btn color="blue darken-1" flat @click.native="close">Cancel</v-btn>
						<v-btn color="blue darken-1" flat @click.native="save">Save</v-btn>
					</v-card-actions>
				</v-card>
			</v-dialog>
		</v-toolbar>

		<v-data-table
			:headers="headers"
			:items="teams"
			hide-actions
			class="elevation-1"
		>
			<template slot="items" slot-scope="props">
				<td>{{ props.item.name }}</td>
				<td class="text-xs-right">{{ props.item.status }}</td>
				<td class="text-xs-right">{{ props.item.progress }} %</td>
				<td class="text-xs-right">{{ props.item.spv }}</td>
				<td class="text-xs-right">{{ props.item.countdown }}</td>
				<td class="justify-center layout px-0">
					<v-icon
						small
						class="mr-2"
						@click="editItem(props.item)"
					>
						edit
					</v-icon>
					<v-icon
						small
						@click="deleteItem(props.item)"
					>
						delete
					</v-icon>
				</td>
			</template>
			<template slot="no-data">
				<v-btn color="primary" @click="initialize">Reset</v-btn>
			</template>
		</v-data-table>
	</div>
</template>

<script>
	import moment from 'moment'
	export default {
		props: [
			'projectProps'
		],
		data: () => ({
			statusList: [
				'WIP',
				'WAPP',
				'LOCK'
			],
			dialog: false,
			headers: [
				{
					text: 'Name',
					align: 'left',
					sortable: false,
					value: 'name'
				},
				{ text: 'Status', value: 'status' },
				{ text: 'Progress', value: 'progress' },
				{ text: 'Supervisor', value: 'spv' },
				{ text: 'Countdown', value: 'countdown' },
				{ text: 'Actions', value: 'name', sortable: false }
			],
			teams: [],
			editedIndex: -1,
			editedItem: {
				name: '',
				status: 0,
				progress: 0,
				spv: '',
				countdown: 0,
				subs: []
			},
			defaultItem: {
				name: '',
				status: 0,
				progress: 0,
				spv: '',
				countdown: 0,
				subs: []
			},

			project: {}
		}),

		computed: {
			formTitle () {
				return this.editedIndex === -1 ? 'New Team' : 'Edit Team'
			}
		},

		watch: {
			dialog (val) {
				val || this.close()
			}
		},

		created () {
			this.initialize()
		},

		mounted () {
			this.project = this.projectProps;
			this.teams = this.project.teams;
		},

		methods: {
			initialize () {
				this.teams = [
					{
						name: 'Default',
						status: 'WIP',
						progress: 6.0,
						spv: 'Default',
						countdown: 19,
						start: '',
						deadline: '',
						note: '',
						problem: '',
						subs: []
					}
				]
			},

			editItem (item) {
				this.editedIndex = this.teams.indexOf(item)
				this.editedItem = Object.assign({}, item)
				this.dialog = true
			},

			deleteItem (item) {
				const index = this.teams.indexOf(item)
				this.teams.splice(index, 1);
				
				this.project.teams = this.teams;
				this.$root.$emit('save-project', this.project);
			},

			close () {
				this.dialog = false
				setTimeout(() => {
					this.editedItem = Object.assign({}, this.defaultItem)
					this.editedIndex = -1
				}, 300)
			},

			save () {
				this.editedItem.countdown = moment().to(this.editedItem.deadline)
				if (this.editedIndex > -1) {
					Object.assign(this.teams[this.editedIndex], this.editedItem)
				} else {
					this.teams.push(this.editedItem)
				}
				this.project.teams = this.teams;
				this.$root.$emit('save-project', this.project);
				this.close()
			}
		}
	}
</script>