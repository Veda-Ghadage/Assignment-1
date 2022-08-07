<template>
  <div class="home">
    <adduser/>
  </div>
</template>

<script>
import adduser from '@/components/AddUser.vue'

export default {
  name: 'Home',
  components: {
    adduser
  }
}
</script>
