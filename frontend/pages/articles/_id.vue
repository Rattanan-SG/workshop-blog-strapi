<template>
  <div>
    <div
      v-if="article.image"
      id="banner"
      class="uk-height-small uk-flex uk-flex-center uk-flex-middle uk-background-cover uk-light uk-padding"
      :data-src="api_url + article.image.url"
      uk-img
    >
      <h1>{{ article.title }}</h1>
    </div>

    <div class="uk-section">
      <div class="uk-container uk-container-small">
        <div
          v-if="article.content"
          id="editor"
          v-html="$md.render(article.content)"
        ></div>
        <p v-if="article.published_at">
          {{ article.published_at }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import articleQuery from '~/apollo/queries/article/article'

export default {
  data() {
    return {
      article: {},
      api_url: process.env.strapiBaseUri
    }
  },
  apollo: {
    article: {
      prefetch: true,
      query: articleQuery,
      variables() {
        return { id: parseInt(this.$route.params.id) }
      }
    }
  }
}
</script>
