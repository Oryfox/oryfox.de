<template>
  <main>
    <h1 class="w-full p-4 text-8xl font-bold flex justify-center lg:justify-start lg:text-[12rem] text-teal-900 dark:text-teal-200">{{ user.login }}</h1>
    <h2 class="hidden lg:block w-full px-6 mb-[-2rem] mt-8 text-2xl text-teal-900 dark:text-teal-200 font-semibold">{{ user.bio }}</h2>

    <Divider classes="mx-4 bg-teal-600 dark:bg-teal-100/25 lg:mt-14" />

    <div class="lg:grid grid-cols-3">
      <div class="bg-teal-200 dark:bg-teal-900 rounded-xl p-4 m-4 mt-8 flex flex-col" v-for="repo in repositories"
        :key="repo.id">
        <h2 class="text-teal-700 dark:text-teal-200 font-semibold text-3xl truncate">{{ repo.name }}</h2>
        <Divider classes="bg-teal-400 dark:bg-teal-200/25" />
        <p class="text-teal-700 dark:text-teal-200 text-xl font-semibold grow">
          {{ repo.description }}
        </p>
        <Divider classes="" />
        <div class="flex items-center justify-between">
          <a class="text-teal-600 dark:text-teal-300" :href="repo.html_url">View on GitHub</a>
          <a :href="repo.homepage" v-if="repo.homepage" class="text-teal-500 dark:text-teal-300">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16">
              <path
                d="M8.707 1.5a1 1 0 0 0-1.414 0L.646 8.146a.5.5 0 0 0 .708.708L2 8.207V13.5A1.5 1.5 0 0 0 3.5 15h9a1.5 1.5 0 0 0 1.5-1.5V8.207l.646.647a.5.5 0 0 0 .708-.708L13 5.793V2.5a.5.5 0 0 0-.5-.5h-1a.5.5 0 0 0-.5.5v1.293L8.707 1.5ZM13 7.207V13.5a.5.5 0 0 1-.5.5h-9a.5.5 0 0 1-.5-.5V7.207l5-5 5 5Z" />
            </svg>
          </a>
        </div>
        <div>
          <Divider classes="bg-teal-400 dark:bg-teal-200/25" />
          <div class="flex mt-2 gap-2 flex-wrap" v-if="repo.topics.length > 0">
            <div v-for="topic in repo.topics" class="bg-teal-600 border border-teal-900 rounded-xl px-2 text-teal-200">
              {{ topic }}
            </div>
          </div>
          <div class="text-teal-600" v-else>
            No topics
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
let userName = import.meta.env.VITE_GITHUB
export default {
  async created() {
    // For rate limiting reasons it is recommended to use the provided example files
    // fetch('/repos.json')
    //   .then(response => response.json())
    //   .then(data => {
    //     this.repositories = data
    //   })

    // fetch('/user.json')
    //   .then(response => response.json())
    //   .then(data => {
    //     this.user = data
    //   })

    fetch(`https://api.github.com/users/${userName}/repos`)
      .then(response => response.json())
      .then(data => {
        this.repositories = data
      })

    fetch(`https://api.github.com/users/${userName}`)
      .then(response => response.json())
      .then(data => {
        this.user = data
      })
  },
  data() {
    return {
      user: {},
      repositories: []
    }
  }
}
</script>