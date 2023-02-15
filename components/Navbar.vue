<template>
  <nav class="h-14 bg-slate-500 sticky top-0 z-20 shadow border-b border-b-gray-700">
    <div class="container mx-auto py-2">
      <ul class="flex gap-2">
        <li
          class="p-2 border rounded hover:bg-slate-700 hover:text-white duration-75 cursor-pointer"
        >
          <NuxtLink to="/">Inicio</NuxtLink>
        </li>
        <li
          class="p-2 border rounded hover:bg-slate-700 hover:text-white duration-75 cursor-pointer"
        >
          <NuxtLink to="/nosotros">Nosotros</NuxtLink>
        </li>
      </ul>
    </div>
  </nav>
</template>
