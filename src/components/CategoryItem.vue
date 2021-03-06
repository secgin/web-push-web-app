<template>
  <div :class="{ [category.class]: true }">
    <span>
      <i :class="{ [category.icon]: true }" class="fab fa-2x"></i>
      <span>{{ category.title }} - {{ category.id }}</span>
    </span>
    <button @click="subscribe">Takip Et</button>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'CategoryItem',
  props: ['category'],
  data () {
    return {
      serviceWorker: null
    }
  },
  methods: {
    async subscribe () {
      this.serviceWorker = await navigator.serviceWorker.ready
      const clientId = await this.serviceWorker.pushManager.subscribe({
        userVisibleOnly: true,
        applicationServerKey:
          'BBvtgfsznUadqpaIj3Yo4rWnzUgS8CWiy30BRokLiKewTRA_0i3DizTGgbv02O9BXZFAMm2o1mGpfJVeM9Pk1Zo'
      })

      axios
        .post(`http://localhost:3000/subscribe/${this.category.id}`, {
          subscriber: clientId
        })
        .then(res => {
          console.log('Category_sub_response', res)
        })
    }
  },
  async created () {
    this.serviceWorker = await navigator.serviceWorker.register('./sw.js')
  }
}
</script>
