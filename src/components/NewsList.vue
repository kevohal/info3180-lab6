<template>
    <ul class="news__list">
        <li v-for="article in articles" class="news__item">
            <!-- <img :src="image" class="news__item"/> -->
            <!-- {{ image }} -->
            <h3>{{ article.title }}</h3>
            <p>{{ article.description}}</p>

        </li>
    </ul>
</template>

<script>

export default {
    data() {
        return {
            articles: [],
            // image: {image: url(article.urlToImage)}
        };
            
        

        },
        created() {
            let self = this;

            fetch('https://newsapi.org/v2/top-headlines?country=us&apiKey=fb043ad247004c06b50523a5db684dd0' ,
    {
        headers: {
            Authorization: `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
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
}
</script>