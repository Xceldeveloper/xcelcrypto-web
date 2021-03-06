<template>
  <div id="navbar" class="border-b-2 border-gray-100 relative bg-white">
    <div class="max-w-7xl mx-auto px-4 sm:px-6">
      <div
        class="flex justify-between items-center py-6 md:justify-start md:space-x-10"
      >
        <div class="flex justify-start lg:w-0 lg:flex-1">
          <a href="https://github.com/Xceldeveloper/xcelcrypto-web">
            <img
              class="h-8 w-auto sm:h-10"
              src="https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png"
              alt="git"
            />
          </a>
        </div>

        <div class="hidden md:flex items-center justify-end md:flex-1 lg:w-0">
          <a
            href="https://xceldeveloper/.com"
            class="whitespace-nowrap text-base font-medium text-gray-500 hover:text-gray-900"
          >
            Xcelcrypto
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    name:"navbar"

}
</script>

<style scoped>
#navbar{
    width:100%;
     box-shadow: 0px 2px 10px lightgrey;
}
</style>