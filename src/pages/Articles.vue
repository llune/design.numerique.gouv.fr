<template>
  <Layout class="articles-page">

    <div class="cover">
     <div class="cover__container">

       <h1 class="text-highlight"><Blog class="h1__icon" focusable="false" aria-hidden="true"/>Articles</h1>

      </div>
    </div>

    <div class="content">

        <section class="articles">
          <article v-for="{ node } in $page.allArticle.edges" :key="node.id">
            <g-image :src="node.illustration" focusable="false" alt="" aria-hidden="true"/>
            <p class="articles__date">{{ node.publishedDate }}</p>
            <h2><g-link :to="node.path">{{ node.title }}</g-link></h2>
            <p>{{ node.description }}</p>
          </article>
        </section>

    </div>

  </Layout>
</template>

<page-query>

  query {
    allArticle (sortBy: "publishedDate", order: DESC) {
      edges {
        node {
        	id
          title
          publishedDate (format: "D MMMM YYYY", locale : "fr")
          illustration
          description
          path
        }
      }
    }
  }

</page-query>

<script>

  import Blog from "~/assets/images/blog.svg"

  export default {
    components: {
      Blog,
    },
    metaInfo: {
      title: "Articles",
      meta: [{
        name: "description",
        content: "Découvrez nos dernières publications sur le design et l'accessibilité numérique."
      },
      {
        property: "og:title",
        content: "Articles - DesignGouv"
      },
      {
        property: "og:description",
        content: "Découvrez nos dernières publications sur le design et l'accessibilité numérique."
      },
      {
        property: "og:image",
        content: "https://design.numerique.gouv.fr/designGouv.png"
      },
      {
        name: "twitter:card",
        content: "summary_large_image"
      },
      {
        name: "twitter:site",
        content: "@Design_Gouv"
      },
      {
        name: "twitter:title",
        content: "Articles - DesignGouv"
      },
      {
        name: "twitter:description",
        content: "Découvrez nos dernières publications sur le design et l'accessibilité numérique."
      },
      {
        name: "twitter:image",
        content: "https://design.numerique.gouv.fr/designGouv.png"
      }],
    }
  }

</script>

<style lang="scss">

  @import "src/assets/scss/_vars.scss";

  .articles-page {

    .cover {
      margin-bottom: 80px;

      @media only screen and (max-width: $mobile-max-width) {
        margin-bottom: 48px;
      }

    }

    h2 {
      a {
        border-bottom: none !important;
      }
    }

  }

</style>
