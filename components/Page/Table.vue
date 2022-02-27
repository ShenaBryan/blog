<template>
  <div
    class="p-2 flex flex-col justify-start items-start space-y-2 w-full md:w-96"
  >
    <div class="border-zinc-400 border-2 p-4 md:w-72 w-full">
      <ol class="space-y-2 list-decimal list-inside">
        <li class = "p-2"><a class="text-pamred-100" :href="`#`">{{ news.title }}</a></li>
        <li
          v-for="heading in news.body.children
            .filter((x) => x.tag === 'h2')
            .map((x) => ({ name: x.children[1].value, id: x.props.id }))"
          :key="heading.id"
          class="p-2"
        >
          <a class="text-pamred-100" :href="`#${heading.id}`">{{
            heading.name
          }}</a>
        </li>
      </ol>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    news: {
      type: Object,
      default: null,
    },
  },
}
</script>