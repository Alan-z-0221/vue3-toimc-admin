<template>
  <t-card class="p-4">
    <h3 class="text-lg leading-6 font-medium text-gray-900 mb-2">画廊列表</h3>

    <ul
      role="list"
      class="grid grid-cols-2 gap-x-4 gap-y-8 sm:grid-cols-3 sm:gap-x-6 lg:grid-cols-4 xl:gap-x-8"
    >
      <li v-for="file in files" :key="file.source" class="relative">
        <div
          class="group block w-full aspect-w-10 aspect-h-7 rounded-lg bg-gray-100 focus-within:ring-2 focus-within:ring-offset-2 focus-within:ring-offset-gray-100 focus-within:ring-indigo-500 overflow-hidden"
        >
          <img
            :src="file.source"
            alt=""
            class="object-cover pointer-events-none group-hover:opacity-75"
          />
          <button type="button" class="absolute inset-0 focus:outline-none">
            <span class="sr-only">View details for {{ file.title }}</span>
          </button>
        </div>
        <p class="mt-2 block text-sm font-medium text-gray-900 truncate pointer-events-none">{{
          file.title
        }}</p>
        <p class="block text-sm font-medium text-gray-500 pointer-events-none">{{ file.size }}</p>
      </li>
    </ul>
  </t-card>
</template>

<script lang="ts">
  import axios from 'axios'
  import { Random } from 'mockjs'

  export default defineComponent({
    setup() {
      onMounted(async () => {
        const res = await axios.get('/api/public/beauty')
        console.log('🚀 ~ file: gallery.vue ~ line 37 ~ onMounted ~ res', res.data)
        if (res && res.data) {
          files.value = res.data.data.map((o) => ({
            title: Random.cname(),
            size: '',
            source: o
          }))
        }
      })

      const files = ref([
        {
          title: 'IMG_4985.HEIC',
          size: '3.9 MB',
          source: ''
        }
      ])

      return {
        files
      }
    }
  })
</script>

<style scoped></style>
