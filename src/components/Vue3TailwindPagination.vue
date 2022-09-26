<template>
  <div v-if="total_pages > 1"
       class="bg-white px-4 py-3 flex text-xs items-center justify-between sm:px-6">
    <div class="flex-1 flex justify-between sm:hidden">
      <nav class="relative z-0 inline-flex rounded-md -space-x-px" aria-label="Pagination">
         <span>
            <a @click="changePage(1)"
               :class="`relative mr-1 inline-flex rounded-full cursor-pointer shadow-sm text-sm items-center px-1 py-2 border ${border_color} ${background} text-sm font-medium ${color}`">
            First
          </a>
         </span>

        <span>
            <a @click="changePage(current_page - 1)"
               :class="`relative mr-1 inline-flex rounded-full shadow-sm text-sm items-center px-2 py-2 border ${border_color} ${background} text-sm font-medium ${color}`">
            <span class="sr-only">Previous</span>
            <svg class="h-5 w-5 cursor-pointer" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
              <path fill-rule="evenodd"
                    d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z"
                    clip-rule="evenodd"/>
            </svg>
          </a>
          </span>

        <span v-for="(page, index) in reducedData" :key="index">
            <a :class="[current_page == page ? `${active_background} ${active_color} border ${active_border_color}` :  `${background} border ${border_color}`]"
               class="relative inline-flex items-center mr-1 px-4 py-2 rounded-full cursor-pointer shadow-sm bg-white text-sm text-gray-700"
               @click.prevent="changePage(page)">
                <span :class="[current_page == page ? 'text-white' :  '']">{{ page }}</span>
            </a>
          </span>

        <span>
            <a @click="changePage(current_page + 1)"
               :class="`relative inline-flex items-center mr-1 px-2 py-2 rounded-full shadow-sm bg-white text-sm border ${border_color} ${color} ${background}`">
            <span class="sr-only">Next</span>
            <svg class="h-5 w-5 cursor-pointer" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
              <path fill-rule="evenodd"
                    d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
                    clip-rule="evenodd"/>
            </svg>
          </a>
          </span>

        <span>
            <a @click="changePage(total_pages)"
               :class="`relative inline-flex items-center cursor-pointer px-1 py-2 rounded-full shadow-sm bg-white text-sm border ${border_color} ${color} ${background}`">
            Last
          </a>
          </span>
      </nav>
    </div>
    <div class="hidden sm:flex-1 sm:flex sm:items-center sm:justify-between">
      <span v-if="show_text">
        <p class="text-sm text-gray-700">
          {{ text.one }}
          <span class="font-medium">{{ current_page }}</span>
          {{ text.two }}
          <span class="font-medium">{{ total_pages }}</span>
          {{ text.three }}
          <span class="font-medium">{{ total }}</span>
          {{ text.four }}
        </p>
      </span>
      <div>
        <nav class="relative z-0 inline-flex rounded-md -space-x-px" aria-label="Pagination">
         <span class="hidden lg:block">
            <a @click="changePage(1)"
               :class="`relative mr-2 inline-flex rounded-full shadow-sm items-center px-2 py-2 border ${border_color} ${background} text-sm font-medium ${color}`">
            <svg fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                 stroke="currentColor" class="w-5 h-5 cursor-pointer">
              <path stroke-linecap="round" stroke-linejoin="round"
                    d="M18.75 19.5l-7.5-7.5 7.5-7.5m-6 15L5.25 12l7.5-7.5"/>
            </svg>
          </a>
         </span>

          <span>
            <a @click="changePage(current_page - 1)"
               :class="`relative mr-2 inline-flex rounded-full shadow-sm items-center px-2 py-2 border ${border_color} ${background} text-sm font-medium ${color}`">
            <span class="sr-only">Previous</span>
            <svg class="h-5 w-5 cursor-pointer" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
              <path fill-rule="evenodd"
                    d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z"
                    clip-rule="evenodd"/>
            </svg>
          </a>
          </span>

          <span v-if="hasFirst()">
            <a :class="`relative cursor-pointer inline-flex items-center rounded-full mr-2 shadow-sm px-4 py-2 border ${border_color} ${background} text-sm font-medium ${color}`"
               @click.prevent="changePage(1)">
              <span>
                1
              </span>
            </a>
          </span>

          <a @click="less()"
             class="relative inline-flex items-center cursor-pointer px-4 py-2 mr-2 ml-1 bg-white text-sm font-medium text-gray-700"
             v-if="hasFirst()">...</a>

          <span v-for="(page, index) in pages" :key="index">
            <a :class="[current_page == page ? `${active_background} ${active_color} border ${active_border_color}` :  `${background} border ${border_color}`]"
               class="relative inline-flex items-center mr-2 px-4 py-2 rounded-full cursor-pointer shadow-sm bg-white text-sm font-medium text-gray-700"
               @click.prevent="changePage(page)">
                <span :class="[current_page == page ? 'text-white' :  '']">{{ page }}</span>
            </a>
          </span>

          <a @click="more()"
             class="relative inline-flex cursor-pointer mr-2 items-center px-4 py-2 text-sm font-medium text-gray-700"
             v-if="showLast()">...</a>
          <span>
            <a @click="changePage(current_page + 1)"
               :class="`relative inline-flex items-center mr-2 px-2 py-2 rounded-full shadow-sm bg-white text-sm font-medium border ${border_color} ${color} ${background}`">
            <span class="sr-only">Next</span>
            <svg class="h-5 w-5 cursor-pointer" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
              <path fill-rule="evenodd"
                    d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
                    clip-rule="evenodd"/>
            </svg>
          </a>
          </span>

          <span class="hidden lg:block">
            <a @click="changePage(total_pages)"
               :class="`relative inline-flex items-center px-2 py-2 rounded-full shadow-sm bg-white text-sm font-medium border ${border_color} ${color} ${background}`">
            <svg fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                 stroke="currentColor" class="w-5 h-5 cursor-pointer">
              <path stroke-linecap="round" stroke-linejoin="round"
                    d="M11.25 4.5l7.5 7.5-7.5 7.5m-6-15l7.5 7.5-7.5 7.5"/>
            </svg>
          </a>
          </span>
        </nav>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Vue3TailwindPagination',
  data() {
    return {
      page_range: 2
    }
  },
  props: {
    current_page: {
      type: Number,
      default: 1
    },
    total: {
      type: Number,
      default: 79
    },
    per_page: {
      type: Number,
      default: 5
    },
    background: {
      type: String,
      default: 'bg-gray-200'
    },
    active_background: {
      type: String,
      default: 'bg-gray-900'
    },
    color: {
      type: String,
      default: 'text-gray-500'
    },
    active_color: {
      type: String,
      default: 'text-white'
    },
    border_color: {
      type: String,
      default: 'border-transparent'
    },
    active_border_color: {
      type: String,
      default: 'border-transparent'
    },
    show_text: {
      type: Boolean,
      default: false
    },
    text: {
      default: {
        one: 'Enregirstrements',
        two: 'à',
        three: 'de',
        four: 'resultats'
      }
    },
  },
  methods: {
    hasFirst: function () {
      return this.rangeStart !== 1
    },
    hasLast: function () {
      return this.rangeEnd < this.total_pages
    },
    showLast: function () {
      return this.rangeEnd < this.total_pages && this.total_pages - this.current_page > 2
    },
    changePage: function (page) {
      if (page > 0 && page <= this.total_pages) {
        this.$emit('change', page)
      }
    },
    more() {
      this.changePage(this.current_page + this.page_range)
    },
    less() {
      this.changePage(this.current_page - this.page_range)
    }
  },
  computed: {
    pages: function () {
      let pages = []
      for (let i = this.rangeStart; i <= this.rangeEnd; i++) {
        pages.push(i)
      }
      return pages
    },
    reducedData: function () {
      return this.pages[this.pages.length - 1] > 3 ? this.pages.slice(1) : this.pages;
    },
    rangeStart: function () {
      const start = this.current_page - this.page_range + 1
      return (start > 0 && start != this.page_range) ? start : 1
    },
    rangeEnd: function () {
      const end = this.current_page + this.page_range - 1
      return (end + 1 <= this.total_pages) ? end : this.total_pages
    },
    total_pages: function () {
      return this.per_page >= 1 ? Math.ceil(this.total / this.per_page) : Math.ceil(this.total / 10)
    },
  }
}
</script>