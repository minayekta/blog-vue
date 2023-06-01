<template>
     <div class="col-lg-8">
                <div v-if="! loading">
                    <!-- Featured blog post-->
                    <post :post="posts[0]"></post>
                    <!-- Nested row for non-featured blog posts-->
                    <div class="row">
                        <div class="col-lg-6" v-for="(postGroup , index) in posts.slice(1)" :key="index">
                            <!-- Blog post-->
                            <post v-for="post in postGroup" :key="post.id" :post="post"></post>
                        </div>
                    </div>
                </div>
                <div v-else>loading</div>
                <pagination :currentPage="page.current" :totalPage="page.totalPage" @pagechanged="changePage"></pagination>
            </div>
</template>

<script>
import Post from './Post.vue'
import axios from 'axios';
import _ from 'underscore';
import Pagination from './Pagination.vue';

export default {
    components : {
        Post,
        Pagination
    },
    data() {
        return {
            posts : null,
            loading : false,
            page : {
                current : 1,
                totalPage : 0
            }
        }
    },
    created() {
        this.getPostData(1)
    },
    methods : {
        changePage(page) {
            this.getPostData(page)
        },
        getPostData(page = 1) {
            this.loading = true;
            axios.get(`https://jsonplaceholder.typicode.com/posts?_page=${page}&_limit=9`)
                .then(res => {
                    this.loading = false;
                    this.posts = res.data;
                    let mainPost = this.posts.shift()


                    this.posts = [mainPost , ..._.chunk(this.posts,  2)]
                    this.page.current = page;
                    this.page.totalPage = parseInt(parseInt(res.headers['x-total-count']) / 9)
                    console.log(this.page)
                })
                .catch(err => console.log(err))
        }
    }
}
</script>