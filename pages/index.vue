<template>
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
    const article = await $content(`blog/first`).fetch()
    return {
      article,
    }
  },
}
</script>
