<template>
  <div class="container p-10 bg-gray-100">
    <div class="overflow-x-hidden bg-gray-100">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-3">
        <div
          class="md:p-8 p-2 bg-white rounded-xl"
          v-for="post of posts"
          :key="post"
        >
          <nuxt-link :to="{ name: 'slug', params: { slug: post.slug } }">
            <img
              class="rounded-lg w-full"
              src="https://images.unsplash.com/photo-1603349206295-dde20617cb6a?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=750&q=80"
            />

            <p class="text-indigo-500 font-semibold text-base mt-2">Science</p>

            <h1
              class="font-semibold text-gray-900 leading-none text-xl mt-1 capitalize truncate"
            >
              {{ post.title }}
            </h1>
            <div class="max-w-full">
              <p class="text-base font-medium tracking-wide text-gray-600 mt-1">
                {{ post.description }}
              </p>
            </div>
            <div class="flex items-center space-x-2 mt-20">
              <img
                class="w-10 h-10 object-cover object-center rounded-full"
                src="https://randomuser.me/api/portraits/men/54.jpg"
                alt="random user"
              />
              <div>
                <p class="text-gray-900 font-semibold">Lugano Shabani</p>
                <p class="text-gray-500 font-semibold text-sm">
                  Feb 24,2021 &middot; 6 min read
                </p>
              </div>
            </div>
          </nuxt-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const posts = await $content("posts", params.slug)
      .only(["title", "description", "slug"])
      .sortBy("createdAt", "asc")
      .fetch();
    return { posts };
  },
};
</script>