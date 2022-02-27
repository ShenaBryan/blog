<template>
  <div class="p-8">
    <div class="text-lg">
      <div class="
          flex
          md:flex-row md:space-x-12
          flex-col
          items-stretch
          md:justify-between
          justify-start
        ">
        <div class="py-2 w-full">
          <div class="
              p-2
              text-white
              font-semibold
              border-gray-400 border-b-2
            ">
            Recent Posts:
          </div>
          <div class="flex flex-col md:flex-row md:flex-wrap space-y-4 md:space-y-0 md:space-x-4 items-start w-full px-2">
            <div
              v-for="article in articles"
              :key="article.url.toLowerCase()"
              class="p-4 w-full md:w-72"
            >
              <div class="flex flex-col items-stretch space-y-4 bg-zinc-900 shadow-md transition duration-500 ease-in-out transform hover:translate-y-1">
                <div class="object-cover">
                  <img :src="article.banner" />
                </div>
                <div class="flex flex-col items-stretch space-y-4 shadow-md p-4">

                  <NuxtLink :to="`/posts/${article.url.toLowerCase()}`">{{ article.title }}
                  </NuxtLink>
                  <div class="text-xs">{{article.created.substring(0, 10).split("-").reverse().join(" - ")}}</div>

                  <div class="text-sm">{{article.description}}</div>
                  
                </div>
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
  async asyncData({ $content }) {
    function getMS(d) {
      return new Date(d).getTime()
    }
    let articles = await $content('blog').fetch()
    if (Array.isArray(articles))
      articles = articles
        .sort((a, b) => getMS(a.createdAt) - getMS(b.createdAt))
        .reverse()
    else articles = [articles]
    return {
      articles,
    }
  },
}
</script>


<!--<template>
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
          <div class="md:flex flex-row items-start justify-between px-2">
            <div class="flex flex-col items-start w-full order-1">
              <PageArticle :news="article" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ params, $content }) {
    const article = await $content(`main`).fetch()
    return {
      article,
    }
  },
}
</script>
-->