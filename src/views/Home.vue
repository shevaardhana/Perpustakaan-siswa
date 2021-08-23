<template>
  <div class="home">
    <Header />
    <Books />
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/components/Header.vue'
import Books from '@/components/Books.vue'

export default {
  name: 'Home',
  components: {
    Header,
    Books
  }
}
</script>
