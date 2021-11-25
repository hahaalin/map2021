<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>

  <div
    class="
      bg-purple
      sm:bg-green
      md:bg-blue md:text-yellow
      lg:bg-red
      xl:bg-orange
    "
  >
    Test
  </div>

  <div
    class="
      p-6
      max-w-sm
      mx-auto
      bg-white
      rounded-xl
      shadow-md
      flex
      items-center
      space-x-4
    "
  >
    <div class="flex-shrink-0">
      <img
        class="h-12 w-12"
        src="https://images.unsplash.com/photo-1622645789666-5ec9dcc7accd?auto=format&fit=crop&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&q=80&w=634"
        alt="ChitChat Logo"
      />
    </div>
    <div>
      <div class="text-xl font-medium text-black">ChitChat</div>
      <p class="text-gray-500">You have a new message!</p>
    </div>
  </div>
</template>
