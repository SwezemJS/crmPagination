# crmPagination
Простая пагинация на Vue.js
***
 Install
=====================
**Global:** 
```
Vue.component('Pagination',require('./components/pagination.vue').default)
```
**Local:** 
```
import Pagination from './components/Pagination.vue'
```
 Setting
=====================
**`perPage`** - total number of pages.

**`curPage`** - current page :)

Renderer
=====================
```
<pagination
    v-bind:perPage="YOU_VARIABLE_TOTAL"
    v-bind:curPage="YOU_VARIABLE_PERRENT"
    v-on:YOU_EMIT="YOU_FUNCTION(YOU_PARAMENTR)"
    v-if="isLoad">
</pagination>```