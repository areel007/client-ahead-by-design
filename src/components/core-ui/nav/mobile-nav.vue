<template>
  <ul
    class="mobile-nav"
    v-if="isMobileNavVisible"
  >
    <svg
      height="24px"
      viewBox="0 0 24 24"
      width="24px"
      fill="#000000"
      class="close"
      @click="$emit('close')"
    >
      <path d="M0 0h24v24H0V0z" fill="none"/>
      <path d="M19 6.41L17.59 5 12 10.59 6.41 5 5 6.41 10.59 12 5 17.59
      6.41 19 12 13.41 17.59 19 19 17.59 13.41 12 19 6.41z"/>
    </svg>
    <li
      v-for="(navLink, index) in navLinks"
      :key="index"
      @click="$emit('go-to')"
    >
      <router-link :to="navLink.to">{{ navLink.link }}</router-link>
    </li>
  </ul>
</template>

<script lang="ts">
import {defineComponent} from "vue";

export default defineComponent({
  name: "mobile-nav",
  props: ["navLinks", "isMobileNavVisible"],
});
</script>

<style scoped>
.mobile-nav {
  width: 100%;
  height: 100vh;
  background-color: #0e0e0e;
  z-index: 100;
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: space-around;
  flex-direction: column;
}
.mobile-nav li {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.mobile-nav li a {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  color: var(--color-white);
  text-decoration: none;
  font-size: var(--fs-14);
}
.mobile-nav li a:before {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  transition: .5s ease;
  background-color: #282828;
}
.mobile-nav li a:hover:before {
  width: 100%;
  z-index: -10;
}
.close {
  position: absolute;
  top: 1rem;
  right: 1rem;
  fill: var(--color-white);
  z-index: 100;
  cursor: pointer;
}
</style>
