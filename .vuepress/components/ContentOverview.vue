<template>
    <section>
        <ul>
            <li v-for="article in articles()">
                <a :href="article.path">{{articleDate(article)}} - {{article.title}}</a>
            </li>
        </ul>
    </section>
</template>

<script>
const dateFormat = require('dateformat');

export default {
    methods: {
        articles() {
            return this.$site.pages
            .filter((page) => page.path.startsWith("/articles/") && page.frontmatter.status == 'published' && page.frontmatter.date)
            .sort((a, b) => new Date(b.frontmatter.date) - new Date(a.frontmatter.date));
        },
        articleDate(article) {
            return dateFormat(new Date(article.frontmatter.date), "dd-mm-yyyy");
        }
    },
}
</script>
