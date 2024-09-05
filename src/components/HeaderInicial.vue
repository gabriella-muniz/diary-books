<template>
    <div>
      <header class="bg-gradient-to-r from-teal-400 to-blue-200 p-4 shadow-md">
        <div class="container mx-auto flex justify-between items-center">
          <span class="text-white text-3xl font-font">Book Diary</span>
          <nav>
            <ul class="hidden md:flex space-x-6 font-font">
              <li>
                <a
                  href="/"
                  class="text-white hover:text-gray-300 transition-colors duration-300 cursor-pointer"
                >Início</a>
              </li>
              <li>
                <a
                  href="/suggestions"
                  class="text-white hover:text-gray-300 transition-colors duration-300 cursor-pointer"
                >Sugestões</a>
              </li>
             
            </ul>
            <!-- Menu responsivo -->
            <div class="md:hidden">
              <button
                @click="menuOpen = !menuOpen"
                class="text-white focus:outline-none"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                  class="w-6 h-6"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M4 6h16M4 12h16M4 18h16"
                  />
                </svg>
              </button>
            </div>
          </nav>
        </div>
        <!-- Menu mobile -->
        <div
          v-if="menuOpen"
          class="md:hidden bg-gradient-to-r from-teal-300 to-blue-100 p-4 space-y-2 mt-2 font-font"
        >
          <div
            v-for="(item, index) in menuItems"
            :key="index"
            class="p-2 rounded-lg hover:bg-yellow-100 transition-colors duration-300"
          >
            <a
              :href="item.href"
              class="block text-gray text-lg cursor-pointer"
            >
              {{ item.text }}
            </a>
          </div>
        </div>
      </header>
    </div>
  </template>
  
  <script>
  export default {
    name: 'HeaderInicial',
    data() {
      return {
        menuOpen: false,
        menuItems: [
          { text: 'Início', href: '/' },
          { text: 'Sugestões', href: '/tasks' },
          
        ],
      };
    },
  };
  </script>
  
  