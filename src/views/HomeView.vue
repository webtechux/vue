<template>
  <div class="home">
  <TabWrapper/>
  </div>
</template>

<script>
// @ is an alias to /src
import TabWrapper from '@/components/DashBoard.vue'

export default {
  name: 'HomeView',
  components: {
    TabWrapper
  }
}
</script>
