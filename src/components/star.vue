<template>
    <div class='star'>
        <ul class='star_list'>
            <li class='star_item' :class='{"pos":index<num}' v-for='(item,index) in 5' :key='item' @click='handleClick(index)' @mousemove='handlemove(index)' @mouseout='out(index)'></li>
        </ul>
    </div>
</template>
<script>
export default {
  name: 'satr',
  data () {
    return {
      num: 0,
      saveNum: 0
    }
  },
  methods: {
    handleClick (index) {
      this.num = index + 1
      this.saveNum = index + 1
      this.$emit('starLevel', this.num)
    },
    handlemove (index) {
      this.num = index + 1
    },
    out (index) {
      this.num = this.saveNum
    }
  },
  props: ['score'],
  mounted () {
    this.num = this.score
    this.saveNum = this.num
  }
}
</script>
<style scoped>

ul {
    display: flex;
    align-items: center;
    width: auto;
}

ul,
li {
    padding: 0;
    margin: 0;
    height: 15px;
}

li {
    list-style-type: none;
    float: left;
    cursor: pointer;
}

.star_item {
    width: 15px;
    height: 15px;
    background-image: url(../assets/star.png);
    background-repeat: no-repeat;
    background-position: -17px 0px;
    background-size: cover;
}
.pos{
    background-position: 0px;
}
</style>


