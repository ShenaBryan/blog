<template>
<div class = "bg-zinc-800">
  <div class="p-8">
    <div class="text-lg">
      <div
        class="
          flex
          md:flex-row md:space-x-12
          flex-col
          items-stretch
          md:justify-between
          justify-start
        "
      >
        <div class="py-2 w-full">
          <div
            class="
              p-2
              text-white
              font-semibold
              border-zinc-400 border-b-2
            "
          >
            {{ article.title }}
          </div>
          <div class = "p-4 text-sm">{{formatDate(article.createdAt)}}</div>
          <div class="md:flex flex-row items-start justify-between px-2">
            <div class="flex flex-col items-start w-full md:w-auto order-2">
              <PageTable :news="article" />
            </div>
            <div class="flex flex-col items-start w-full order-1">
              <PageArticle :news="article" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  head() {
    return {
        title: this.article.title,
        meta: [
          {
            hid: 'description',
            name: 'description',
            content: this.article.description
          },
          {
            hid: 'og-image',
            name: 'og:image',
            content: this.article.banner
          }
        ]
      }

  },
  async asyncData({ params, $content }) {
    const article = await $content(`blog/${params.title}`).fetch()
    return {
      article,
    }
  },
  methods: {
    formatDate(d) {
      return new Date(d).toUTCString()
    }
  }
}
</script>
