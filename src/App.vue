<script>
import { ref, reactive, computed } from 'vue'
import { Vue3TailwindPagination } from './components/';

export default {
  components: {
    Vue3TailwindPagination
  },
  setup() {
    const page = ref(1)
    const total = ref(79)

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
 <vue3-tailwind-pagination :total="total" :per_page="5" :current_page="page" @change="onChange" />
</template>