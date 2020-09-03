<template>
  <div class="sprpag">
    <div class="text pag-inline" @click="downPage()">
      <i class="mr-3px las la-long-arrow-alt-left"></i>
      Пред.
    </div>
    <div v-for="item in list">
      <div v-if="item == pag_current"  class="pag-inline pag-active" @click="selectPage(item)"> {{ item }}</div>
      <div v-else class="pag-inline" @click="selectPage(item)">{{ item }}</div>
    </div>
    <div class="pr-3px pl-3px" v-if="(pag_current != pag_total)&& (pag_total-3) > pag_current">...</div>
    <div class="pr-3px pl-3px" @click="selectPage(pag_total)" v-if="(pag_current != pag_total)&& (pag_total-3) > pag_current">{{ pag_total }}</div>
    <div class="text pag-inline" @click="upPage()">
      След.
      <i class="ml-3px las la-long-arrow-alt-right"></i>
    </div>

  </div>
</template>

<script>
export default {
  props:['perPage','curPage'],
  data () {
    return {
      pag_total: this.perPage,
      pag_current: this.curPage,
      list:[]
    }
  },
  methods:{
    selectPage(item) {
      this.pag_current = item;
    },
    downPage() {
      if (this.pag_current-1 != 0) {
        this.pag_current -= 1;
      }
    },
    upPage() {
      if (this.pag_current+1 <= this.pag_total) {
        this.pag_current += 1;
      }
    },
    createList(){
      this.list = [];
      if ((this.pag_current == 1) && this.pag_current < this.pag_current) {
        for (let i = this.pag_current;i<=this.pag_current+3;i++) {
          if (i == this.pag_current || i >= this.pag_total){
            break;
          } else {
            this.list.push(i);
          }
        }
      } else {
        for (let i = this.pag_current-3;i<=this.pag_current+3;i++) {
          if (i > 0 && i <= this.pag_total) {
            this.list.push(i);
          } else {
            continue;
          }
        }
      }
    },
  },
  beforeMount() {
    this.createList();
  },
  watch:{
    pag_current: function (){
      this.createList();
      this.$emit('getPageId', this.pag_current);
    }
  }
}
</script>

<style scoped>
.sprpag > div {
  display: inline;
}
.pag-inline {
  display: inline-block;
  margin: 0 5px 0 5px;
  cursor: pointer;
}
.pag-active {
  color: white;
  background: #6979f8;
  border: 1px solid black;
  border-color: #6979f8;
  border-radius: .3846rem;
  padding: 5px;
}

</style>