<script>
export default {
	name: 'ProjectCard',

	props: {
		project: Object,
		base_api_url: String,

	},

	data() {
		return {




		}
	},
}
</script>
<template>


	<div class="txt_color">


		<div class="
			text-decoration-none txt_color">
			<div class="txt_color text-center py-4 title_projects">
				<a :href="project.code" target="_blank" class="text-decoration-none">
					<span class="px-4"> {{ project.create_data }} </span>
					<span class="title_show">{{ project.title }}</span>
					<span class="px-4" v-if="project.type"> / Type: {{ project.type ? project.type.name : 'no type'
						}}</span>
				</a>

			</div>
		</div>

		<!-- <router-link :to="{ name: 'show', params: { id: project.id, slug: project.slug } }" class="
			text-decoration-none txt_color">
			<div class="txt_color text-center py-4 title_projects">
				<span class="px-4"> {{ project.create_data }} </span>
				<span class="title_show">{{ project.title }}</span>
				<span class="px-4" v-if="project.type"> / Type: {{ project.type ? project.type.name : 'no type'
					}}</span>

			</div>
		</router-link> -->







	</div>


</template>
<style></style>