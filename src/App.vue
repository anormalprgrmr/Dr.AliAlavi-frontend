<script>
import loginForm from './components/loginForm.vue'
import AdminPanel from './components/AdminPanel.vue'
import Home from './components/Home.vue'
import Requset from './components/Requset.vue'

export default {
  components: {
    loginForm,
    AdminPanel,
    Home,
    Requset
  },
  data() {
    return {
      currentPage: 'home'
    }
  },
  methods: {
    updateParentData(page) {
      this.currentPage = page; // Update parent data
    }
  }
  // methods:{
  //   setCur(state){
  //     this.
  //   }
  // }
}
</script>

<template>
  <Transition>
    <loginForm @update-data="updateParentData" v-if="this.currentPage == 'login'"></loginForm>
  </Transition>
  <Transition>
    <AdminPanel @update-data="updateParentData" v-if="this.currentPage == 'admin'"></AdminPanel>
  </Transition>
  <Transition>
    <Home @update-data="updateParentData" v-if="this.currentPage == 'home'"></Home>
  </Transition>
  <Transition>
    <Requset @update-data="updateParentData" v-if="this.currentPage == 'request'"></Requset>
  </Transition>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
