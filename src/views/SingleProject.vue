<script>
import ProjectCard from '../components/ProjectCard.vue';
import AppBanner from '../components/AppBanner.vue';
import axios from 'axios';

export default {
	name: 'SingleProject',
	components: {
		ProjectCard,
		AppBanner,
	},

	data() {
		return {
			base_api_url: 'https://back.muttimatteo.com/api/projects',
			base_project_url: '',
			project: '',
			loading: true,
		}
	},
	methods: {
		callApi(url) {
			axios.get(url)
				.then(response => {
					console.log(response);
					if (response.data.success) {
						console.log(response.data.response);
						this.project = response.data.response;
						this.loading = false;
					} else {
						this.$router.push({ name: 'not-found' })
					}

				})
				.catch(err => {
					console.error(err);
				})
		},



	},
	mounted() {
		console.log(this.base_api_url, this.base_project_url, `/${this.$route.params.slug}`);
		let url = this.base_api_url + this.base_project_url + `/${this.$route.params.slug}`;
		this.callApi(url);

	}
}
</script>
<template>

	<div>
		<div class="text-center">
			<h2 class="">{{ project.title }}</h2>
		</div>
		<div class="text-center video_section">
			<section>
				{{ project.description }}
			</section>



		</div>
		<!--  
		<div class="text-center">
			<img :src="'https://back.muttimatteo.com/api/projects/storage/' + project.cover_image" alt="" class="py-4">
		</div>
		<div class="text-end p-4">
			{{ project.description }}
		</div>

		<div class="d-flex justify-content-between p-4">
			<div class="">
				{{ project.code }}
			</div>
		</div>
			-->
		<div class="text-center">
			{{ project.repo }}
		</div>

		<div class="p-4" v-if="project.technologies">
			<div class="text-center" v-for="tech in project.technologies">
				{{ tech.name }}
			</div>
		</div>
		<div class="text-center p-4" v-if="project.type">
			{{ project.type.name }}
		</div>
	</div>

</template>
<style>
.video_section {}
</style>