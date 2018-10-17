<template lang="pug">
  v-app(dark)
    v-navigation-drawer(app light)
    v-toolbar(app)
      toolbar-content
    v-content
      v-container(fluid).grey.elevation-5
        router-view(v-if="user.id !== 0")
        login(v-else)
    v-footer(app)
</template>

<script>
import ToolbarContent from './ToolbarContent.vue';
import Login from './Login.vue';
import {mapGetters, mapMutations} from 'vuex';
export default {
  components: {
    ToolbarContent,
    Login
  },
  computed: {
    ...mapGetters(['user'])
  },
}
</script>
