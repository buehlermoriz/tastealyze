<template>
  <!-- component -->
<header>
    <nav class="bg-white shadow">
        <div class="container mx-auto px-6 py-5 ">
            <div class="md:flex md:items-center md:justify-between">
                <div class="flex justify-between items-center">
                    <div class="text-xl font-semibold text-gray-700">
                     <img class="block h-12 w-auto " src="./assets/tastealyze-logo.png" alt="tastealyze" />
                        
                    </div>

                    <!-- Mobile menu button -->
                    <div class="flex md:hidden">
                        <button type="button" class="text-gray-500 hover:text-gray-600 focus:outline-none focus:text-gray-600" aria-label="toggle menu">
                            <svg viewBox="0 0 24 24" class="h-6 w-6 fill-current">
                                <path fill-rule="evenodd" d="M4 5h16a1 1 0 0 1 0 2H4a1 1 0 1 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2z"></path>
                            </svg>
                        </button>
                    </div>
                </div>

                 <!-- Mobile Menu open: "block", Menu closed: "hidden" -->
                <div class="hidden -mx-4 md:flex md:items-center">
                    <a href="#" class="block mx-4 mt-2 md:mt-0 text-sm text-gray-700 capitalize hover:text-blue-600">Allgemeine Informationen</a>
                    <a href="#" class="block mx-4 mt-2 md:mt-0 text-sm text-gray-700 capitalize hover:text-blue-600">Rotwein</a>
                    <a href="#" class="block mx-4 mt-2 md:mt-0 text-sm text-gray-700 capitalize hover:text-blue-600">Weißwein</a>
                    <a href="#" class="block mx-4 mt-2 md:mt-0 text-sm text-gray-700 capitalize hover:text-blue-600">Rosé</a>
                </div>
            </div>
        </div>
    </nav>

    <div class="w-full bg-cover bg-center" style="height:55rem; background-image: url(https://images.unsplash.com/photo-1562601579-599dec564e06?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80);">
        <div class="flex items-center justify-center h-full w-full bg-gray-900 bg-opacity-50">
            <div class="text-center">
                <h1 class="text-white text-2xl font-semibold uppercase md:text-3xl">The taste of <span class="text-red-400">WINE</span></h1>
              <!--  <button class="mt-4 px-4 py-2 bg-blue-600 text-white text-sm uppercase font-medium rounded hover:bg-blue-500 focus:outline-none focus:bg-blue-500">Start project</button> -->
            </div> 
        </div> 
    </div>
</header>

       

       <div x-data="setup()" x-init="$refs.loading.classList.add('hidden');">
      <div class="flex h-screen antialiased text-gray-900 bg-gray-100 dark:bg-dark dark:text-light">
       

        <!-- Sidebar -->
        <div
          class="fixed inset-y-0 z-10 flex w-80"
        >
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
                 <img class="block h-12 w-auto " style="padding-left:40px;" src="./assets/tastealyze-logo.png" alt="tastealyze" />
              </a>
            </div>

            <nav class="flex flex-col flex-1 w-64 p-4 mt-4" >
              <a href="#"  class="flex items-center space-x-2" >
            
                  <a href="#" class="block mx-12 mt-2 md:mt-0 text-s text-black-700 capitalize hover:text-red-600">Home</a>
                  <a href="rotwein" class="block mx-12 mt-2 md:mt-0 text-s text-black-700 capitalize hover:text-red-600">Rotwein</a>
                  <a href="weisswein" class="block mx-12 mt-2 md:mt-0 text-s text-black-700 capitalize hover:text-red-600">Weißwein</a>
                  <a href="rose" class="block mx-12 mt-2 md:mt-0 text-s text-black-700 capitalize hover:text-red-600">Rosé</a>
              </a>
            </nav>
          </div>
        </div>
        
      </div>
    </div>



</template>
