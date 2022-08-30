<script>
import { ref, reactive, computed } from 'vue'
import { Vue3TailwindPagination } from './components/';

export default {
  components: {
    Vue3TailwindPagination
  },
  setup() {
    const page = ref(1)
    const total = ref(75)

    // expose to template and other options API hooks
    return {
      page,
      total
    }
  },

  methods: {
    onChange(page) {
      this.page = page
    }
  }
}
</script>

<template>
 <vue3-tailwind-pagination :total="total" :current_page="page" @change="onChange" />
</template>