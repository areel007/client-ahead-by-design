<template>
  <div class="home">
    <web-view-nav
      :nav-links="navLinks"
      :is-logged-in="isLoggedIn"
      @open="open"
    ></web-view-nav>
    <mobile-nav
      :nav-links="navLinks"
      @close="close"
      :is-mobile-nav-visible="isMobileNavVisible"
      @go-to="goTo"
    ></mobile-nav>
    <router-view></router-view>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from "vue";
import WebViewNav from "@/components/core-ui/nav/web-view-nav.vue";
import MobileNav from "@/components/core-ui/nav/mobile-nav.vue";

export default defineComponent({
  name: "Home",
  components: { MobileNav, WebViewNav },
  setup() {
    const navLinks = reactive(
      [
        {
          to: "/",
          link: "Home"
        },
        {
          to: "services",
          link: "Services"
        },
        {
          to: "projects",
          link: "Projects"
        },
        {
          to: "contact",
          link: "Contact"
        },
        {
          to: "register",
          link: "Blog"
        },
      ]
    )

    const isLoggedIn = ref(false)

    const isMobileNavVisible = ref(false)

    /** Methods */

    const close = () => {
      isMobileNavVisible.value = false
    }

    const open = () => {
      isMobileNavVisible.value = true
    }

    const goTo = () => {
      isMobileNavVisible.value = false
    }

    return {
      navLinks,
      isLoggedIn,
      close,
      isMobileNavVisible,
      open,
      goTo,
    }
  }
});
</script>

<style scoped>
.home {
  position: relative;
}
</style>
