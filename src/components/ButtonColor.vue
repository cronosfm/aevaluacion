<template>
  <Button v-bind:style="[colors]" @click="activar"> {{ id }}</Button>
</template>

<script>
export default {
  name: "ButtonColor",
  props: {
    id: {
      type: Number,
      required: true,
    },
    color: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      colors: "{ 'background-color': '#FFFFFF' }",
    };
  },
  methods: {
    activar() {
      console.log("no");
      this.colors = this.color;
      setInterval(() => {
        this.colors = "{ 'background-color': '#FFFFFF' }";
      }, 1000);
    },
    verificar() {
      console.log("si funciono");
    },
  },
};
</script>

<style>
button {
  height: 30vh;
  width: 33%;
}
</style>