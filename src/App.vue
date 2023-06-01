<template>
        <my-nav></my-nav>
        <my-header></my-header>

        <!-- Page content-->
        <div class="container">
           
            <div class="row">
                <!-- Blog entries-->
                <post-list></post-list>
                <sidebar></sidebar>
            </div>
        </div>

        <my-footer></my-footer>

</template>

<script>
  import Header from './components/layouts/Header.vue';
  import Nav from './components/layouts/Nav.vue';
  import Footer from './components/layouts/Footer.vue';
  import Sidebar from './components/layouts/Siderbar.vue';
  import PostList from './components/PostList.vue'


  export default {
    components : {
      'my-nav' :Nav,
      'my-header' : Header ,
      'my-footer' : Footer,
      PostList,
      Sidebar
    }
  }
</script>