<template>
	<v-layout>

		<!-- Sidebar -->
		<v-flex md2>
			<v-navigation-drawer permanent>
				<v-toolbar flat>
					<v-list>
						<v-list-tile>
							<v-list-tile-title class="title">
							{{currentDate}}
							</v-list-tile-title>
						</v-list-tile>
					</v-list>
				</v-toolbar>

				<v-divider></v-divider>
				
				<!-- Project time range -->
				<div class="pa-3">
					Start: 18 Sep 2018 <br>
					Deadline: 1 Des 2018
				</div>
				
				<!-- Project info -->
				<div class="pa-3">
					<ul>
						<li>Project: "Die Hard Fans"</li>
						<li>Status: WIP</li>
						<li>Progress: 80%</li>
						<li>Countdown: 90 days</li>
						<li>Note: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde eius fugit omnis quisquam itaque debitis, aspernatur at ullam, quaerat nihil repellat, rem, deserunt illum atque iste commodi aliquid incidunt! At!</li>
						<li>Problem: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Minus, explicabo, soluta. Quia, magnam incidunt quae, suscipit eos dicta ratione blanditiis modi sapiente, possimus fuga eveniet non. Nesciunt eaque enim, culpa.</li>
					</ul>
				</div>
				
				<!-- Time Schedule -->
				<div class="pa-3">
					<h3>Time Schedule</h3>
					<ul>
						<li>Team Animation: 
							<ul>
								<li>Time: 18 Sep - 20 Sep</li>
								<li>Countdown: 90 days</li>
							</ul>
						</li>
						<li>Team Concept: 
							<ul>
								<li>Time: 18 Sep - 20 Sep</li>
								<li>Countdown: 90 days</li>
							</ul>
						</li>
						<li>Team Story: 
							<ul>
								<li>Time: 18 Sep - 20 Sep</li>
								<li>Countdown: 90 days</li>
							</ul>
						</li>
					</ul>
				</div>

			</v-navigation-drawer>
		</v-flex>

		<!-- Main Content -->
		<v-flex md10>
			<div class="header pa-3">
				<h1>{{title}} | <small>Week 1 - Team Animation <span class="grey--text">(Riyak)</span></small></h1>
			</div>
			<v-container>
				
				<!-- Note, Problem, Info -->
				<v-layout>
					<v-flex md5>
						<v-card>
							<v-card-title>Note</v-card-title>
							<v-card-text>
								Lorem ipsum dolor sit amet, consectetur adipisicing elit. Animi aspernatur repellat, totam, expedita amet architecto doloremque porro maxime qui! Quaerat possimus earum soluta tempora magnam, officiis quasi obcaecati illo in!
							</v-card-text>
						</v-card>
					</v-flex>
					<v-flex md5>
						<v-card>
							<v-card-title>Problem</v-card-title>
							<v-card-text>
								Lorem ipsum dolor sit amet, consectetur adipisicing elit. Animi aspernatur repellat, totam, expedita amet architecto doloremque porro maxime qui! Quaerat possimus earum soluta tempora magnam, officiis quasi obcaecati illo in!
							</v-card-text>
						</v-card>
					</v-flex>

					<!-- Team info -->
					<v-flex md2>
						<v-card>
							<v-card-title>Problem</v-card-title>
							<v-card-text>
								<ul>
									<li>Status: WIP</li>
									<li>Progress: 80%</li>
									<li>Countdown: 90 days</li>
								</ul>
							</v-card-text>
						</v-card>
					</v-flex>
				</v-layout>
				
				<v-divider class="my-3"></v-divider>

				<!-- Subs -->
				<v-card class="mb-1">
					<v-card-title>Animation A</v-card-title>
					<v-card-text>
						<!-- Info -->
						<v-layout>
							<v-flex md5>
								<p><b>Note</b>: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde eius fugit omnis quisquam itaque debitis, aspernatur at ullam, quaerat nihil repellat, rem, deserunt illum atque iste commodi aliquid incidunt! At!</p>
							</v-flex>
							<v-flex md5>
								<p><b>Problem</b>: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Minus, explicabo, soluta. Quia, magnam incidunt quae, suscipit eos dicta ratione blanditiis modi sapiente, possimus fuga eveniet non. Nesciunt eaque enim, culpa.</p>
							</v-flex>
							<v-flex md2>
								<ul>
									<li>Status: WIP</li>
									<li>Progress: 80%</li>
									<li>Countdown: 90 days</li>
								</ul>
							</v-flex>
						</v-layout>
					</v-card-text>
				</v-card>

				<v-card class="mb-1">
					<v-card-title>Animation B</v-card-title>
					<v-card-text>
						<!-- Info -->
						<v-layout>
							<v-flex md5>
								<p><b>Note</b>: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde eius fugit omnis quisquam itaque debitis, aspernatur at ullam, quaerat nihil repellat, rem, deserunt illum atque iste commodi aliquid incidunt! At!</p>
							</v-flex>
							<v-flex md5>
								<p><b>Problem</b>: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Minus, explicabo, soluta. Quia, magnam incidunt quae, suscipit eos dicta ratione blanditiis modi sapiente, possimus fuga eveniet non. Nesciunt eaque enim, culpa.</p>
							</v-flex>
							<v-flex md2>
								<ul>
									<li>Status: WIP</li>
									<li>Progress: 80%</li>
									<li>Countdown: 90 days</li>
								</ul>
							</v-flex>
						</v-layout>
					</v-card-text>
				</v-card>

				<v-card class="mb-1">
					<v-card-title>Animation C</v-card-title>
					<v-card-text>
						<!-- Info -->
						<v-layout>
							<v-flex md5>
								<p><b>Note</b>: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde eius fugit omnis quisquam itaque debitis, aspernatur at ullam, quaerat nihil repellat, rem, deserunt illum atque iste commodi aliquid incidunt! At!</p>
							</v-flex>
							<v-flex md5>
								<p><b>Problem</b>: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Minus, explicabo, soluta. Quia, magnam incidunt quae, suscipit eos dicta ratione blanditiis modi sapiente, possimus fuga eveniet non. Nesciunt eaque enim, culpa.</p>
							</v-flex>
							<v-flex md2>
								<ul>
									<li>Status: WIP</li>
									<li>Progress: 80%</li>
									<li>Countdown: 90 days</li>
								</ul>
							</v-flex>
						</v-layout>
					</v-card-text>
				</v-card>

			</v-container>
		</v-flex>
	</v-layout>
</template>

<script>
	import moment from 'moment';
	export default {
		data: function(){
			return {
				title: 'Die Hard Fans',
				author: 'Does University',
				currentDate: ''
			}
		},
		mounted: function(){
			this.currentDate = moment().format('DD MMM YYYY');
		}
	}
</script>