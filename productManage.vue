<template>
  <div class="zm-product-content">
    <setProductType></setProductType>
    <productSelect v-if="isproductSelect"></productSelect>
    <EasyScrollbar v-if="isproduct">
      <div class="zm-dialog-pageBox" :style="{height:isheight}">
        <ul class="zm-dialog-pageList">
          <productType v-for="(item,i) in setList" :key="i" :prop="item" tarIndex=1></productType>
        </ul>
      </div>
    </EasyScrollbar>
    <productCheck></productCheck>
  </div>
</template>
<style scoped lang="less" src="./productManage.less">
</style>
<script>
import setProductType from "./setProductType";
import productType from "./productType";
import productSelect from "./setProductSelect";
import productCheck from "./setProductCheck";
export default {
  name: "product-manage",
  components: {
    setProductType,
    productType,
    productSelect,
    productCheck
  },
  data() {
    return {
      isheight: "524px",
      isproduct: true,
      isproductSelect: true,
      current: null,
      lists: []
    };
  },
  beforeCreate() {
    let url =
      "http://local.zuma.com/product/webbuilder-api/productCategory/getProductCategoryList";
    let _this = this;
    _this.$axios
      .get(
        url,
        {},
        {
          headers: {
            "Content-Type": "application/json;charset=utf-8"
          }
        }
      )
      .then(function(response) {
        let result = response.data.data;
        _this.lists = result;
        console.log("数据OK!", result);
      })
      .catch(error => {
        console.log(error);
      });
  },
  computed: {
    setList() {
      let _this = this;
      curData(_this.lists);
      function curData(_data) {
        _data.forEach(item => {
          if (item.list == null && item.list == undefined || item.list.length==0) {
             item.isCheck = true;
          } else {
            curData(item.list);
          }
        });
      }
       console.log(this.lists,"///////////////////")
      return _this.lists;
    }
  }
};
</script>

