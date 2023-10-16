<template>
    <div class="articles">
        <div v-for="article in data.articles" class="article">
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
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: row;
    flex-wrap: wrap;
}
.article{
    padding: 10px 10px;
}

.article-card{
    border: 1px solid black;
    padding: 0px 10px;
}

.title{
    font-weight: 600;
}

.author{
    font-size: 0.8rem;
    color: gray;
}
</style>