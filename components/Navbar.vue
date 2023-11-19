<script setup>
import { ref, reactive } from 'vue';
const mobilenav = ref(false);
const showhide = function () {
  mobilenav.value = !mobilenav.value
}

const subtoggle = function (sub) {
  sub.isActive = !sub.isActive;
}


const menus = reactive(
  [
    {
      name: 'Home',
      link: '/',
      isActive: false,
    },
    {
      name: 'Link One',
      link: '/one',
      isActive: false,
    },
    {
      name: 'Link Two',
      link: '/two',
      isActive: false,
    },
    {
      name: 'Three Sub',
      link: '/three',
      isActive: false,
      sub: [{
        name: 'Sub One',
        link: '/subone',
        isActive: false,
      },
      {
        name: 'Sub Two',
        link: '/subtwo',
        isActive: false,
      },
      {
        name: 'Sub Three',
        link: '/subthree',
        isActive: false,
      }]
    },
    {
      name: 'Link Four',
      link: 'four',
      isActive: false,
    },
    {
      name: 'Link Sub',
      link: '/five',
      isActive: false,
      sub: [{
        name: 'Sub One',
        link: '/subone',
        isActive: false,
      },
      {
        name: 'Sub Two',
        link: '/subtwo',
        isActive: false,
      },
      {
        name: 'Sub Three',
        link: '/subthree',
        isActive: false,
      }]
    }
  ]
);
</script>

<template>
  <header class="text-gray-600 body-font">
    <div class="flex justify-between border-b px-4 py-6 block md:hidden">
      <div class="text-4xl leading-4" v-if="mobilenav" @click="showhide">&#215;</div>
      <div @click="showhide" class="space-y-2" v-if="!mobilenav">
        <div class="w-8 h-0.5 bg-gray-600"></div>
        <div class="w-8 h-0.5 bg-gray-600"></div>
        <div class="w-8 h-0.5 bg-gray-600"></div>
      </div>
      <a href="/">
        <Logo class="px-4 block md:hidden" />
      </a>
    </div>

    <div v-if="mobilenav" class="flex md:hidden flex-col justify-between border-e bg-white">
      <div class="px-4 py-6">
        <ul class="mt-0 space-y-1">
          <li v-for="(menu, index) in menus" :key="index" class=" border-b relative">
            <span class="flex">
              <button v-if="menu.sub" @click="subtoggle(menu.sub)"
                class="text-left block px-4 py-2 text-sm font-medium text-gray-700 flex-1">
                {{ menu.name }}
              </button>
              <a v-else :href="menu.link" class="block px-4 py-2 text-sm font-medium text-gray-700 flex-1">
                {{ menu.name }}
              </a>
              <span class="py-2">
                <svg v-if="menu.sub" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20"
                  fill="currentColor">
                  <path fill-rule="evenodd"
                    d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                    clip-rule="evenodd" />
                </svg>
              </span>
            </span>
            <ul v-if="menu.sub" v-show="menu.sub.isActive" class="space-y-1">
              <li v-for="(sub, index) in menu.sub" :key="index">
                <a class="px-4 py-2 block text-sm font-medium text-gray-700 flex-1" :href="sub.link">{{ sub.name }}</a>
              </li>
            </ul>
          </li>
        </ul>
      </div>

      <div class="sticky inset-x-0 bottom-0 border-t border-gray-100">
        <a href="#" class="flex items-center gap-2 bg-white p-4 hover:bg-gray-50">
          <div>
            <p class="text-xs">
              <strong class="block font-medium">Copyright &copy; 2024</strong>
              <span> https://activelava.net </span>
            </p>
          </div>
        </a>
      </div>
    </div>

    <div class="container mx-auto hidden md:flex flex-wrap p-5 flex-col md:flex-row items-center">
      <a class="flex title-font font-medium items-center text-gray-900 mb-4 md:mb-0">
        <Logo />
      </a>
      <nav class="md:ml-auto flex flex-wrap items-center text-base justify-center">
        <li class="list-none relative" :class="{ group: menu.sub }" v-for="menu in menus" :key="menu.id">
          <a :href="menu.link" class="mr-5 hover:text-gray-900">
            {{ menu.name }}
          </a>
          <ul v-if="menu.sub" class="hidden group-hover:block absolute w-[250px] bg-white">
            <li v-for="(sub, index) in menu.sub" :key="index">
              <a href="#">{{ sub.name }}</a>
            </li>
          </ul>
        </li>
      </nav>
    </div>
  </header>
</template>