<template>
  <input type="text" v-model="todo" @keydown="handleSubmit" />
</template>

<script>
export default {
  data: function () {
    return {
      todo: "",
    };
  },
  methods: {
    handleSubmit: function (e) {
      if (e.keyCode !== 13) return;
      console.log(this.todo);
      this.$emit("submit", this.todo);
      this.todo = "";
    },
  },
};
</script>

<style lang="scss" scoped></style>
