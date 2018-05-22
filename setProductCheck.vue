<template>
  <div class="zm-dialog-check">
    <button class="zm-dialog-check-button">{{title}}</button>
  </div>
</template>
<script>
export default {
  name: "set-product-check",
  props: ["prop"],
  data() {
    return {
      title:"管理产品"
    };
  },
  methods: {

  }
};
</script>

