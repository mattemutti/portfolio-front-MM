<script>
import ProjectCard from '../components/ProjectCard.vue';
import AppBanner from '../components/AppBanner.vue';
import axios from 'axios';

export default {
	name: 'AppProjects',
	components: {
		ProjectCard,
		AppBanner,
	},

	data() {
		return {
			base_api_url: 'https://forge.laravel.com',
			base_project_url: '/api/v1/servers/829590/databases/1182003',
			projects: [],
			loading: true,
			id: [],

		}
	},
	methods: {
		callApi(url) {
			axios.get(url, {
				headers: {
					'Authorization': 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiIxIiwianRpIjoiMzM0YzFiYTliNzM4MTc2ZGY4N2ViZTMxYTJhNDllMTg3Y2Y2NWVmOGY5MWVjMjJlN2FjNzcwZGM4ZGM1NTk1MjU0Y2QwNmIyZGFjY2RmYTYiLCJpYXQiOjE3MjMxODc4MzcuNTU1MTE3LCJuYmYiOjE3MjMxODc4MzcuNTU1MTE5LCJleHAiOjIwMzg3MjA2MzcuNTM3NDU5LCJzdWIiOiIyMzE1NTciLCJzY29wZXMiOltdfQ.j50XPLohV4f5JigoYU6yIP1meEbtcBql_39iOLtHmYHP8x_ds5hFNvYsgFl8DS5EJFYyy3BUWY1rxsL_uT7hQibyFXnfQca_zQraxZaC1aV9mzhezWSPddqenm4TOfafbGOlw9 - kIqDbaVMEqdSXfqhtgdiE_ahthBz7WTLXJGr2OrKA0lvRsoHICXY2VzbEacYSH8haEfVZvyzsg9O0LMQAf38tjtF7dSGNLftc4b5kMhlqp0_JOusjGXOP9uH7kbsv7ZLfeUzLKd2YT_xdu79jGWFu4N3AzqfA4B8KhmGiG1S - 8MAioTn2pwSJHXk2ha94hpFgi1rEVw2Nm_dnK7sdWIiWn7urlYDpfoxTwWWcUoHsmRoCIkOfaiGrjlOi9qlZydfKbGe4o8R3C5smEextq5a8_87eOwOp5fcOy5MiXzvtQY1oKFUMhxh3sCgVnThs1fDMMveKOWxJP_DB5teXHuL2MwThBaMHsyGb8tvIBgrOPtnjZAolAHM4HYU6IPF6tCXg0FDG3XfvNcq1w1- yjtX93w8O1_3jAnh_E9Q7AxW03OrilcPJU - MVQ9dJ3Zqs5LEc8ZN5_xUxoW282oWYJ604zppWteWH776NLKW8dQkQN9iQWtnygBMAc_YeSJtkIKNjXEjD_a0y5y0FRBzvh - yxed0RGdL1zQXcdxI',
				},
			})
				.then(response => {
					auth: {
						username = uname
						password = pass
					}
					console.log(response);
					this.projects = response.data.projects;
					this.loading = false;
				})
				.catch(err => {
					console.error(err);
				})
		},

		nextPage(url) {
			//console.log(url);
			this.callApi(url);
		},

		prevPage(url) {
			//console.log(url);
			this.callApi(url);
		},

		goTo(page) {
			const url = this.base_api_url + this.base_project_url + `?page=${page}`
			this.callApi(url);
		},

		showProject(id) {

		}
	},
	mounted() {
		console.log(this.base_api_url, this.base_project_url);
		let url = this.base_api_url + this.base_project_url;
		this.callApi(url);
	}
}

</script>
<template>
	<div class="container">
		<div class="row" v-if="!loading">
			<ProjectCard v-for="project in  projects.data" :project="project" :key="project.id"
				:base_api_url="base_api_url">

			</ProjectCard>
		</div>
		<div class=" row" v-else>
			<div class="col">
				Loading...
			</div>
		</div>

		<!-- Paginate -->
		<nav aria-label="Page navigation">
			<ul class="pagination d-flex justify-content-between">
				<li class="page-item text_dark" v-show="projects.prev_page_url"
					@click="prevPage(projects.prev_page_url)">
					<button class="page-link text_dark" aria-label="Previous">
						<span class="text-dark" aria-hidden="true">&laquo;</span>
					</button>
				</li>

				<li class="page-item" :class="{ 'active': page == projects.current_page }" :aria-current="page"
					v-for=" page  in  projects.last_page " @click="goTo(page)">
					<button class="page-link text-dark">{{ page }}</button>
				</li>

				<li class="page-item" v-show="projects.next_page_url">
					<button class="page-link" aria-label="Next" @click="nextPage(projects.next_page_url)">
						<span class="text-dark" aria-hidden="true">&raquo;</span>
					</button>
				</li>
			</ul>
		</nav>

	</div>
</template>
<style></style>