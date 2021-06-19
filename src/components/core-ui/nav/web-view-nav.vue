<template>
  <header>
    <div class="container">
      <div class="header__inner">
        <div class="logo"></div>
        <ul>
          <li
            v-for="(navLink, index) in navLinks"
            :key="index">
            <router-link
              :to="navLink.to"
            >{{ navLink.link }}
            </router-link>
          </li>
        </ul>
        <div
          class="user"
          v-if="isLoggedIn"
        ></div>

        <svg
          height="24px"
          viewBox="0 0 24 24"
          width="24px"
          fill="#000000"
          class="hamburger-menu"
          @click="$emit('open')"
        >
          <path d="M0 0h24v24H0V0z" fill="none"/>
          <path d="M3 18h18v-2H3v2zm0-5h18v-2H3v2zm0-7v2h18V6H3z"/>
        </svg>

      </div>
    </div>
  </header>
</template>

<script lang="ts">
import {defineComponent, reactive, ref} from "vue";

export default defineComponent({
  name: "web-view-nav",
  props: ["navLinks", "isLoggedIn"]
});
</script>

<style scoped>
header {
  width: 100%;
  position: fixed;
  background-color: #0e0e0e;
  padding: 1rem 0;
  top: 0;
}
.header__inner {
  width: 100%;
  height: 3rem;
  display: grid;
  grid-template-columns: 1fr 80% 1fr;
  align-items: center;
}
.logo {
  width: 3rem;
  height: 3rem;
  background-color: #fff;
}
.user {
  width: 3rem;
  height: 3rem;
  border-radius: 50%;
  background-color: #fff;
  justify-self: flex-end;
}
.header__inner ul {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  justify-items: center;
  height: 100%;
}
.header__inner ul li {
  height: 100%;
  cursor: pointer;

}
.header__inner ul li a {
  text-decoration: none;
  width: 100%;
  color: #fff;
  height: 100%;
  display: flex;
  justify-items: center;
  align-items: center;
  font-size: 1.2rem;
  letter-spacing: .1rem;
  padding: 0 2rem;
  position: relative;
}
.header__inner ul li a:before {
  content: "";
  height: 100%;
  width: 0;
  background-color: #282828;
  transition: .3s ease;
  position: absolute;
  left: 0;
  z-index: -10;
  opacity: 0;
}
.header__inner ul li a:hover:before {
  width: 100%;
  opacity: 1;
}
.router-link-exact-active {
  background-color: #282828;
}
.hamburger-menu {
  fill: var(--color-white);
  cursor: pointer;
  display: none;
}

@media screen and (max-width: 800px) {
  .header__inner ul {
    display: none;
  }
  .hamburger-menu {
    display: block;
    grid-column: 3/4;
    justify-self: flex-end;
  }
}

</style>
