<template>
  <header>Push Notification</header>
  <div class="app">
    <div class="categories">
      <category-item
        :category="category"
        v-for="category in categoryList"
        :key="category.id"
      />
    </div>
  </div>
</template>
<script>
import axios from "axios";
import CategoryItem from './components/CategoryItem.vue';
export default {
  components: { CategoryItem },
  data() {
    return {
      categoryList: []
    }
  },
  created() {
    axios.get('http://localhost:3000').then(res => {
      this.categoryList = res.data.categoryList;
    })
  }
}
</script>