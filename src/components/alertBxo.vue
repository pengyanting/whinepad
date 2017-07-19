<template>
  <div class='alertBox' ref='box'>
       <section class='boxInner'>
          <header class='header'>
            Add new item
          </header>
          <section class='center'>
             <form>
                <div>
                   <label for="">Name</label>
                   <input type="text" v-model="add.name">
                </div>
                <div>
                   <label for="">Year</label>
                   <input type="number" placeholder="2017" min='1900' v-model="add.year">
                </div>
                <div>
                   <label for="">Grape</label>
                   <select name="" id="" v-model="add.grape">
                      <option :value="item.value" v-for='item in selectList' :key='item'>{{item.value}}</option>
                   </select>
                </div>
                <div>
                   <label for="">Rating</label>
                   <Star :score='add.rating' @starLevel='getLevel'></Star>
                </div>
                <div>
                   <label for="">Commits</label>
                   <textarea name="" id="" cols="20" rows="4" v-model="add.commit"></textarea>
                </div>
             </form>
          </section>
          <footer class='footer'>
             <span @click='cancle'>Cancel</span>
             <div class='btn' @click='addEvent'>Add</div>
          </footer>
       </section>
  </div>
</template>
<script>
import Star from './star.vue'
export default {
  data () {
    return {
      selectList: [
        {value: 'asasa'},
        {value: 'asasa'},
        {value: 'asasa'},
        {value: 'asasa'},
        {value: 'sads'}
      ],
      add: {
        name: '',
        year: '',
        grape: '',
        rating: 0,
        commit: ''
      }
    }
  },
  mounted () {
    this.$refs.box.style.height = document.documentElement.clientHeight + 'px'
  },
  components: {
    Star
  },
  methods: {
    addEvent () {
      this.$emit('add', this.add)
    },
    cancle () {
      this.$emit('cancle')
    },
    getLevel (val) {
      this.add.rating = val
    }
  }
}
</script>
<style scoped>
 .alertBox{
     width: 100%;
     height: 100%;
     background: rgba(0,0,0,.5);
     position: absolute;
     left: 0;
     top: 0;
 }
 .boxInner{
   width: 350px;
   height: 500px;
   position: absolute;
   left:0;top:0;
   right: 0;bottom: 0;
   margin: auto;
 }
 .header {
  width: 100%;
  height: 80px;
  background: #6f001b;
  display: flex;
  align-items: center;
  color: #fff;
  font-family: Norican, cursive;
  padding: 20px;
  font-size: 40px;
}
.btn {
  width: 70px;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: space-around;
  font-size: 20px;
  background: #6f001b;
  border-radius: 50px;
  color: #fff;
  font-weight: 700;
  font-size: 20px;
  padding: 0 10px;
  cursor: pointer;
  margin-left:10px;
}
.footer{
  width: 100%;
  height: 80px;
  background: #fff;
  border-top: 1px solid #ccc;
  display: flex;
  justify-content: flex-end;
  align-items:center;
  padding: 0 10px;
}
.footer span{
  cursor: pointer;
}
.center{
  max-height: 340px;
  overflow-y: auto;
  background: #fff;
  padding: 10px 30px;
}
.center label{
  width: 100%;
  display: block;
  font-size:13px;
  color: #7f7f7f;
  margin-bottom:5px;
  margin-top:10px;
}
.center  input,.center  select{
  padding: 10px;
  outline: none;
  width: 180px;
}
</style>


