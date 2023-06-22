<template>
  <div class="hidden md:block antialiased text-gray-900 dark:bg-dark dark:text-light">
    <div class=" mt-28 pb-28"> 
    <!-- Sidebar -->
    <div class="fixed inset-y-0 z-10 flex w-80">
      <!-- Curvy shape -->
      <svg
        class="absolute inset-0 w-full h-full text-white"
        style="filter: drop-shadow(10px 0 10px #00000030)"
        preserveAspectRatio="none"
        viewBox="60 0 309 800"
        fill="#ffffff"
      >
        <path
          d="M268.487 0H0V800H247.32C207.957 725 207.975 492.294 268.487 367.647C329 243 314.906 53.4314 268.487 0Z"
        />
      </svg>
      <!-- Sidebar content -->

      <div class="z-10 flex flex-col" style="padding-top: 15px">
        <div
          class="flex items-center justify-between flex-shrink-0 w-64 p-4 px-12"
        >
          <img
            class="block h-14 w-auto"
            src="../assets/tastealyze-logo.png"
            alt="tastealyze"
          />
          <a href="#"> </a>
        </div>
        <nav class="flex flex-col w-64 p-4 mt-4">
          <a href="#" class="flex items-center space-x-2">
            <div class="px-10 py-2">
              <button class="flex items-center space-x-3">
                <svg class="w-6 h-6" stroke="currentColor">
                  <path
                    stroke-width="2"
                    d="M6,3l0,6c0,2.97,2.16,5.43,5,5.91V19H8v2h8v-2h-3v-4.09c2.84-0.48,5-2.94,5-5.91l0-6H6z M16,8H8l0-3h8C16,5,16,8,16,8z"
                  />
                </svg>
                <a
                  href="#"
                  class="block text-s text-black-700 capitalize font-semibold hover:text-red-600 active:text-red-600"
                  >Home</a
                >
              </button>
            </div>

            <div class="px-10 py-2">
              <button class="flex items-center space-x-3">
                <svg class="w-6 h-6" stroke="currentColor">
                  <path
                    stroke-width="2"
                    d="M6,3l0,6c0,2.97,2.16,5.43,5,5.91V19H8v2h8v-2h-3v-4.09c2.84-0.48,5-2.94,5-5.91l0-6H6z M16,8H8l0-3h8C16,5,16,8,16,8z"
                  />
                </svg>
                <a
                  href="#introduction"
                  class="block text-s text-black-700 capitalize font-semibold hover:text-red-600 active:text-red-600"
                  >Einführung</a
                >
              </button>
            </div>
            <div class="px-10 py-2">
              <button class="flex items-center space-x-3">
                <svg class="w-6 h-6" stroke="currentColor">
                  <path
                    stroke-width="2"
                    d="M6,3l0,6c0,2.97,2.16,5.43,5,5.91V19H8v2h8v-2h-3v-4.09c2.84-0.48,5-2.94,5-5.91l0-6H6z M16,8H8l0-3h8C16,5,16,8,16,8z"
                  />
                </svg>
                <a
                  href="#wineselector"
                  class="block text-s text-black-700 capitalize font-semibold hover:text-red-600 active:text-red-600"
                  >Weinvergleich</a
                >
              </button>
            </div>
            <div class="px-10 py-2">
              <button class="flex items-center space-x-3">
                <svg class="w-6 h-6" stroke="currentColor">
                  <path
                    stroke-width="2"
                    d="M6,3l0,6c0,2.97,2.16,5.43,5,5.91V19H8v2h8v-2h-3v-4.09c2.84-0.48,5-2.94,5-5.91l0-6H6z M16,8H8l0-3h8C16,5,16,8,16,8z"
                  />
                </svg>
                <a
                  href="#wordcloud"
                  class="block text-s text-black-700 capitalize font-semibold hover:text-red-600 active:text-red-600"
                  >Wordcloud</a
                >
              </button>
            </div>
            <div class="px-10 py-2">
              <button class="flex items-center space-x-3">
                <svg class="w-6 h-6" stroke="currentColor">
                  <path
                    stroke-width="2"
                    d="M6,3l0,6c0,2.97,2.16,5.43,5,5.91V19H8v2h8v-2h-3v-4.09c2.84-0.48,5-2.94,5-5.91l0-6H6z M16,8H8l0-3h8C16,5,16,8,16,8z"
                  />
                </svg>
                <a
                  href="#priceandpoints"
                  class="block text-s text-black-700 capitalize font-semibold hover:text-red-600 active:text-red-600"
                  >Preis</a
                >
              </button>
            </div>
            <div class="px-10 py-2">
              <button class="flex items-center space-x-3">
                <svg class="w-6 h-6" stroke="currentColor">
                  <path
                    stroke-width="2"
                    d="M6,3l0,6c0,2.97,2.16,5.43,5,5.91V19H8v2h8v-2h-3v-4.09c2.84-0.48,5-2.94,5-5.91l0-6H6z M16,8H8l0-3h8C16,5,16,8,16,8z"
                  />
                </svg>
                <a
                  href="#worldmap"
                  class="block text-s text-black-700 capitalize font-semibold hover:text-red-600 active:text-red-600"
                  >Karte</a
                >
              </button>
            </div>
            <div class="px-10 py-2">
              <button class="flex items-center space-x-3">
                <svg class="w-6 h-6" stroke="currentColor">
                  <path
                    stroke-width="2"
                    d="M6,3l0,6c0,2.97,2.16,5.43,5,5.91V19H8v2h8v-2h-3v-4.09c2.84-0.48,5-2.94,5-5.91l0-6H6z M16,8H8l0-3h8C16,5,16,8,16,8z"
                  />
                </svg>
                <a
                  href="#titles"
                  class="block text-s text-black-700 capitalize font-semibold hover:text-red-600 active:text-red-600"
                  >Titel</a
                >
              </button>
            </div>
          </a>
        </nav>
      </div>
    </div>
  </div>
  </div>
</template>

<style scoped>
.nuxt-link-active {
  font-weight: bold;
}
</style>
