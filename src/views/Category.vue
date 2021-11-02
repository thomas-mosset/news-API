<template>
  <div class="category">
    <NewsByCategory />
  </div>
</template>

<script>
import NewsByCategory from '@/components/NewsByCategory.vue';

export default {
  name: 'Category',
  components: {
    NewsByCategory,
  }
}
</script>
