<script>
export default {
  name: 'AppHeader',
  data() {
    return {
      menu: [
        {
          'text': 'Home',
          'route': 'home'
        },
        {
          'text': 'About',
          'route': 'about'
        },
        {
          'text': 'Projects',
          'route': 'projects'
        },
        /*{
          'text': 'Blog',
          'route': 'blog'
        },*/
        {
          'text': 'Contacts',
          'route': 'contacts'
        },
      ]
    }
  }
}

</script>

<template>
  <header>
    <div class="d-flex justify-content-between pb-2">

      <div>
        <div class="text-decoration-none txt_color fs-5">MM</div>
      </div>
      <div class="right-menu d-flex ">
        <router-link :to="{ name: item.route }" v-for="item in menu" class="px-2 text-decoration-none txt_color"
          activeClass="active_menu">
          {{ item.text }}
        </router-link>
      </div>
    </div>


  </header>

</template>

<style></style>
