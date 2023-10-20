<template>
    <div class="articles">
        <div v-for="article in data.articles" class="article">
            <div class="card-image">
                <img :src="article.thumbnailUrl?article.thumbnailUrl:'/img/test.png'" alt="image">
            </div>
            <div class="article-card">
                <p class="title">{{ article.title }}</p>
                <p class="author">Written by: {{ article.author.name }}</p>
            </div>
        </div>
    </div>
</template>

<script setup>
const query = gql`query articlesQuery($per_page: Int!, $page: Int!){
    articles(per_page: $per_page, page: $page){
        title
        slug
        author{
            name
            profilePictureUrl
            username
        }
    }
}`

const variables = { "per_page":10, "page": 1 }

const { data } = await useAsyncQuery(query, variables)

</script>

<style scoped>
.articles{
    margin-top: 64px;
    display: flex;
    justify-content: center;
    flex-direction: row;
    flex-wrap: wrap;
}
.article{
    width: 256px;
    margin: 8px 8px;
    border: 0.5px dotted #000;
}

.article-card{
    padding: 4px 8px;
    background-color: #fff;
}

.card-image img{
    width: 256px;
}

.title{
    font-weight: 700;
    margin-bottom: 8px;
}

.author{
    font-size: 0.8rem;
    color: gray;
    font-weight: 600;
}
</style>