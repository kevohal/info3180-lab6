<template>

    <form @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">

        <div class="input-group mx-sm-3 mb-2">
            <label class="visually-hidden" for="search">Search</label>
            <input type="search" name="search" v-model="searchTerm" id="search"
            class="form-control mb-2 mr-sm-2" placeholder="Enter search term here" />
            <button class="btn btn-primary mb-2">Search</button>
        </div>
        
        <p>You are searching for {{ searchTerm }}</p>

    </form>

    <ul class="news__list">
        <li v-for="article in articles" :key="article.url" class="news__item">
            <img :src="article.urlToImage" class="news__item"/> 
            <h5>{{ article.title }}</h5>
            <p class="para">{{ article.description }}</p> 
        </li>
    </ul>

    

</template>

<script>
export default {
    data() {
        return {
            articles: [],
            searchTerm: ''
        };
    }, 

    methods: {
        searchNews() {
            let self = this;
        
            fetch('https://newsapi.org/v2/everything?q='+ self.searchTerm + '&language=en', 
        
            {
                headers: {
                    Authorization: `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
                }
            })
        }
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

<style>
    ul {   
        display: grid;
        grid-template-columns: repeat(auto-fill,minmax(260px, 1fr));
        row-gap: 10px;
        column-gap: 10px;
        list-style-type: none;
    } 

    .news__item {
        border: solid grey 1px; 
        margin: 15px;
        border-bottom-left-radius: 5%;
        border-bottom-right-radius: 5%;
        border-bottom: solid aqua 5px;
        box-shadow: 3px;
    }

    img.news__item {
        height: 200px;
        width: 278px;
        border-bottom-left-radius: 0;
        border-bottom-right-radius: 0;
        border: 0px;
        align-items: center;
        margin: 0;
        border-left: 0;
        padding: 0;
        
    }

    h5, p.para {
        margin: 5px;
        padding: 5px;
    }
</style>