<template>
  <li :data-index="tarIndex" :style="styleBottom">
    <div class="zm-product-list" :style="styleObject" :data-id="prop.fId">
      <i class="iconfont icon-check" v-if="prop.isCheck" @click="addTarrger(prop)"></i>
      <i class="iconfont icon--jianhao" v-else @click="addTarrger(prop)"></i>
      <span>{{prop.fName}}</span>
    </div>
    <ul>
      <productType v-if="prop.list.length != 0 && prop.list != null" v-for="(item,i) in prop.list" :key="i" :prop="item" :tarIndex="tarIndex-0+1"></productType>
    </ul>
  </li>
</template>
<script>
import productType from "./productType";

export default {
  name: "product-type",
  props: {
    prop: {},
    tarIndex: {
      type: Number,
      default: 1
    }
  },
  data() {
    return {
      tarIndex: this.tarIndex,
      styleObject: {
        paddingLeft: this.tarIndex * 20 + "px"
      },
      styleBottom: {
        borderTop: "1px solid #d7d7d7"
      }
    };
  },
  beforeCreate: function() {
    this.$options.components.productType = require("./productType.vue").default;
  },
  methods: {
    addTarrger(_prop) {
      $(event.currentTarget).toggleClass(function(){
        if ($(this).is(".iconfont.icon--jianhao")) {
          $(this).parent().siblings().toggle();
          $(this)
            .removeClass();
            return "iconfont icon-iconfonticon02";
        } else if($(this).is(".iconfont.icon-check")){
           return "duigouBox";
        }
        else {
          $(this).parent().siblings().toggle();
          $(this)
            .removeClass();
          return "iconfont icon--jianhao";
        }
      });
    }
  },
  mounted() {
    //   console.log( this.zz,'11111111111111111',this.prop.isJianHao,this)
  }
};
</script>
