<template>
    <div class="card mb-4">
        <a href="#!"><img class="card-img-top" src="https://dummyimage.com/700x350/dee2e6/6c757d.jpg" alt="..." /></a>
        <div class="card-body">
            <div class="small text-muted">January 1, 2021</div>
            <h2 class="card-title h4">{{ post.title }}</h2>
            <p class="card-text">{{ post.body }} </p>
            <a class="btn btn-primary" href="#!">Read more →</a>
        </div>
    </div>
</template>


<script>
export default {
    props : ['post']
}
</script>