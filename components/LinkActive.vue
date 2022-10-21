<template>
  <div class="link" @click="getBtnActive(data)">
    <p :class="btnActive.id == data.id ? 'active' : ''">{{ data.text }}</p>
    <img v-if="btnActive.id == data.id" src="/arrow_active.svg" alt="" />
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
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: row;
  margin: 14px 0;
}
.link p {
  margin: 0 !important;
}

.active {
  color: #d8ad3d;
}
</style>
