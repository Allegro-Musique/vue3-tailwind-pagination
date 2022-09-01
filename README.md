# Vue 3 Tailwind Css Pagination

A Vue 3 Tailwind css component for pagination.
## Demo

![alt text](./public/pagination.gif "Vue 3 Tailwind Css pagination")

## Installation

// with npm

`npm i vue-3-tailwind-css-pagination`

## Getting Started

### Import component

```js
import {createApp} from 'vue'
import {Vue3TailwindPagination} from "vue-3-tailwind-css-pagination";

const app = createApp(App)
app.component('Vue3TailwindPagination', Vue3TailwindPagination)

app.mount('#app')
```

### How to use

```html
<vue3-tailwind-pagination 
        :total="79" :per_page="5"
        :active_color="'text-white'"
        :active_background="'bg-red-500'"
        :current_page="pagination.page"
        @change="getPaysheet"/>
```

### Props and attributes

| Id                |  type  |       Default |          Description |
|:------------------|:------:|--------------:|---------------------:|
| total             | Number |            79 | Total count of pages |
| current_page      | Number |             1 |         Current page |
| per_page          | Number |             5 |      Number per page |
| background        | String |   bg-gray-200 |                    - |
| active_background | String |   bg-gray-900 |                    - |
| color             | String | text-gray-500 |                    - |
| active_color      | String |    text-white |                    - |

### Events

| Id     | Output |                            Description |
|:-------|:------:|---------------------------------------:|
| change | Number |      The current page has been updated |