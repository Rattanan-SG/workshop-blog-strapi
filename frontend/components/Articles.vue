<template>
  <div>
    <div class="uk-child-width-1-2" uk-grid>
      <div>
        <router-link
          v-for="article in leftArticles"
          :key="article.id"
          :to="{ name: 'articles-id', params: { id: article.id } }"
          class="uk-link-reset"
        >
          <div class="uk-card uk-card-muted">
            <div v-if="article.image" class="uk-card-media-top">
              <img
                :src="
                  article.image.url[0] == '/'
                    ? api_url + article.image.url
                    : article.image.url
                "
                alt=""
                height="100"
              />
            </div>
            <div class="uk-card-body">
              <p
                v-if="article.category"
                id="category"
                class="uk-text-uppercase"
              >
                {{ article.category.name }}
              </p>
              <p id="title" class="uk-text-large">{{ article.title }}</p>
            </div>
          </div>
        </router-link>
      </div>
      <div>
        <div class="uk-child-width-1-2@m uk-grid-match" uk-grid>
          <router-link
            v-for="article in rightArticles"
            :key="article.id"
            :to="{ name: 'articles-id', params: { id: article.id } }"
            class="uk-link-reset"
          >
            <div class="uk-card uk-card-muted">
              <div v-if="article.image" class="uk-card-media-top">
                <img
                  :src="
                    article.image.url[0] == '/'
                      ? api_url + article.image.url
                      : article.image.url
                  "
                  alt=""
                  height="100"
                />
              </div>
              <div class="uk-card-body">
                <p
                  v-if="article.category"
                  id="category"
                  class="uk-text-uppercase"
                >
                  {{ article.category.name }}
                </p>
                <p id="title" class="uk-text-large">{{ article.title }}</p>
              </div>
            </div>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import articlesQuery from '~/apollo/queries/article/articles'
export default {
  props: {
    articles: {
      type: Array,
      default: () => {
        return { message: 'hello' }
      }
    }
  },
  data() {
    return {
      api_url: process.env.strapiBaseUri
    }
  },
  computed: {
    leftArticlesCount() {
      return Math.ceil(this.articles.length / 5)
    },
    leftArticles() {
      return this.articles.slice(0, this.leftArticlesCount)
    },
    rightArticles() {
      return this.articles.slice(this.leftArticlesCount, this.articles.length)
    }
  }
}
</script>
