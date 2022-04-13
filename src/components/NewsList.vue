<template>
    <ul class="news__list">
        <li v-for="article in articles" class="news__item">
            <!-- <img :src="image" class="news__item"/> -->
            <!-- {{ image }} -->
            <!-- <img src="https://cdn.cnn.com/cnnnext/dam/assets/220411204126-01-kevin-stitt-file-super-tease.jpg" class= "image" />
            {{ image }} -->
            <h5>{{ article.title }}</h5>
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

<style>
    ul { 
    /*    display: flex; 
        flex-direction: column; 
        flex-wrap: nowrap; 
        justify-content: flex-start; 
        margin: 1em 0px; 
        padding: 0; 
        list-style: none; */  
    
    display: grid;
    grid-template-columns: repeat(auto-fill,minmax(250px, 1fr));
    row-gap: 10px;
    column-gap: 10px;
    list-style-type: none;
    
        
} 

.news__item {
    border: solid black 1px; 
    margin: 15px;
    border-bottom-left-radius: 5%;
    border-bottom-right-radius: 5%;
    border-bottom-color: green;

}

/* .image {
    height: 100px;
    width: 250px
} */
    
</style>