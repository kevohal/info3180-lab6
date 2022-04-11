<template>
    <ul class="news__list">
        <li class="news__item">News item 1</li>
        <li class="news__item">News item 2</li>
        <li class="news__item">News item 3</li>
    </ul>
</template>

<script>

export default {
    data() {
        return {};

        },
        created() {
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
            });
        }
//     Authorization: fb043ad247004c06b50523a5db684dd0
}
</script>