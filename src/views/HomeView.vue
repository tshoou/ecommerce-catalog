<template>
  <div class="home">
    <ProductCategory/>
  </div>
</template>

<script>
// @ is an alias to /src
import ProductCategory from '@/components/ProductCategory.vue'

export default {
  name: 'HomeView',
  components: {
    ProductCategory
  }
  }

</script>
