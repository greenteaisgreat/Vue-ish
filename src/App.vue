<script setup>
import { ref } from "vue";

const name = "Nathan";
const year = 2025;
const isDisabled = true;

const favThings = {
  src: "https://lipsum.app/random/500x500",
  alt: "some photo",
};

const things = ["Dreamcast", "3DS", "Soldering"];

const howdy = () => {
  window.alert("Howdy!");
};
</script>

<template>
  <h1>Welcome to my Test Page</h1>
  <div class="wrapper">
    <h3>
      If {{ isDisabled }} is true, then you should see my favorite things:
    </h3>
  </div>
  <div v-if="isDisabled" class="item-wrapper">
    <img v-bind="favThings" />
    <div class="fav-things-wrapper" v-if="isDisabled">
      <p v-for="thing in things" :key="thing">
        {{ thing }}
      </p>
    </div>
  </div>
  <button @click="howdy()">Click me!</button>
  <div>
    <footer>{{ name }} &copy; {{ year }}</footer>
  </div>
</template>

<style scoped>
h1 {
  text-align: center;
  color: white;
  font-weight: bold;
}
footer {
  position: fixed;
  left: 0;
  bottom: 0;
  font-style: monospace;
  width: 100%;
  text-align: right;
}
.wrapper {
  margin: auto;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 5rem;
  color: azure;
}
.item-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1rem;
  margin-top: 1rem;
}
</style>
