<template>
    <ul class="news__list" style = "list-style-type: none;">
        <div class ="pack " style= "display:flex; flex-direction:row; flex-wrap:wrap; justify-content:center;">
        <li v-for="article in articles" class="news__item" style="margin: 10px;">
            
            <div class="card" style="width: 18rem;">
            <img  class="card-img-top" :src="article.urlToImage"  alt="Card image cap"/>
            <div class="card-body">
            {{ article.title }}
            {{ article.description}}
            </div>
            </div>
        </li>
        </div>
    </ul>
</template>


<script>
    export default {
        data() {
            return {
                articles: []
            }
        },
        created() {
        let self = this;
        fetch('https://newsapi.org/v2/top-headlines?country=us',
    {
        headers: {
        'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
    }
    })
    .then(function(response) {
    return response.json();
    })
    .then(function(data) {
    console.log(data);
    self.articles = data.articles;
    });
    }
        
    };
</script>