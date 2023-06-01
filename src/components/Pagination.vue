<template>
     <!-- Pagination-->
    <nav aria-label="Pagination">
        <hr class="my-0" />
        <ul class="pagination justify-content-center my-4">
            <li class="page-item" :class="{ 'disabled' : isInFirstPage }">
                <button type="button" class="page-link" :disabled="isInFirstPage" @click="onClickPage(1)">Newer</button>
            </li>
           
            <li class="page-item" v-for="page in pages" :key="page.name" :class="{ 'active' : page.isActive }">
                <button type="button" @click="onClickPage(page.name)" class="page-link" :disabled="page.isActive">{{ page.name }}</button>
            </li>
      
           
           
            <li class="page-item" :class="{ 'disabled' : isInLastPage }">
                <button type="button" class="page-link" :disabled="isInLastPage" @click="onClickPage(totalPage)">Older</button>
            </li>
        </ul>
    </nav>
</template>

<script>
    export default {
        props : {
            totalPage : {
                type : Number,
                required : true
            },
            currentPage : {
                type:  Number,
                required : true
            },
            maxVisibleButtos : {
                type : Number,
                required : false,
                default : 8
            }
        },
        computed : {
            startPage() {
                if(this.currentPage === 1) return 1;


                if(this.currentPage === this.totalPage) return this.totalPage - 4;


                return this.currentPage - 2;
            },
            endPage() {
                return Math.min(this.startPage + this.maxVisibleButtos - 1, this.totalPage);
            },
            pages() {
                let range = [];

                for (let i = this.startPage ; i <= this.endPage ; i++) {
                    range.push({
                        name : i,
                        isActive : i === this.currentPage 
                    })
                }

                return range;
            },
            isInFirstPage() {
                return this.currentPage === 1;
            },
            isInLastPage() {
                return this.currentPage === this.totalPage;
            }
        },
        methods : {
            onClickPage(page) {
                this.$emit('pagechanged' , page)
            },
        }
    }
</script>