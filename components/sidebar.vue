<template>
  <div class="antialiased text-gray-900 dark:bg-dark dark:text-light">
    <!-- Sidebar -->
    <div class="fixed inset-y-0 z-10 flex w-80">
      <!-- Curvy shape -->
      <svg
        class="absolute inset-0 w-full h-full text-white"
        style="filter: drop-shadow(10px 0 10px #00000030)"
        preserveAspectRatio="none"
        viewBox="0 0 309 800"
        fill="#ffffff"
      >
        <path
          d="M268.487 0H0V800H247.32C207.957 725 207.975 492.294 268.487 367.647C329 243 314.906 53.4314 268.487 0Z"
        />
      </svg>
      <!-- Sidebar content -->
      <div class="z-10 flex flex-col flex-1">
        <div class="flex items-center justify-between flex-shrink-0 w-64 p-4">
          <!-- Logo -->
          <a href="#">
            <img
              class="block h-12 w-auto"
              style="padding-left: 40px;"
              src="../assets/tastealyze-logo.png"
              alt="tastealyze"
            />
          </a>
        </div>
        <nav class="flex flex-col flex-1 w-64 p-4 mt-4">
          <a href="#" class="flex items-center space-x-2">
            <a
              href="#"
              class="block mx-12 mt-2 md:mt-0 text-s text-black-700 capitalize hover:text-red-600"
            >Home</a>
            <a
              href="rotwein"
              class="block mx-12 mt-2 md:mt-0 text-s text-black-700 capitalize hover:text-red-600"
            >Rotwein</a>
            <a
              href="weisswein"
              class="block mx-12 mt-2 md:mt-0 text-s text-black-700 capitalize hover:text-red-600"
            >Weißwein</a>
            <a
              href="rose"
              class="block mx-12 mt-2 md:mt-0 text-s text-black-700 capitalize hover:text-red-600"
            >Rosé</a>
          </a>
        </nav>
      </div>
    </div>
    <!-- Other components -->
    ...
  </div>
</template>
