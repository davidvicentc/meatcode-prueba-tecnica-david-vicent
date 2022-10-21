<template>
  <div class="link" @click="getBtnActive(data)">
    <p :class="btnActive.id == data.id ? 'active' : ''">{{ data.text }}</p>
  </div>
</template>

<script>
export default {
  props: ["btnActive", "data"],

  methods: {
    getBtnActive(data) {
      this.$emit("btnActiveFunction", data);
    },
  },
};
</script>

<style>
.link {
  cursor: pointer;
}
.active {
  color: #d8ad3d;
}
</style>
