<template>
  <div class='alertBox' ref='box'>
       <section class='boxInner'>
          <header class='header'>
            {{title}}
          </header>
          <section class='center' v-if='type=="add"||type=="edit"'>
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
                   <Star :score='rating.rating' @starLevel='getLevel'></Star>
                </div>
                <div>
                   <label for="">Commits</label>
                   <textarea name="" id="" cols="20" rows="4" v-model="add.commit"></textarea>
                </div>
             </form>
          </section>
          <section v-else-if="type=='info'" class='center'>
             <form>
                <div>
                   <label for="">Name</label>
                   <div class='item'>{{info.name}}</div>
                </div>
                <div>
                   <label for="">Year</label>
                    <div class='item'>{{info.year}}</div>
                </div>
                <div>
                   <label for="">Grape</label>
                    <div class='item'>{{info.grape}}</div>
                </div>
                <div>
                   <label for="">Rating</label>
                   <Star :score='info.rating' disabled></Star>
                </div>
                <div>
                   <label for="">Commits</label>
                    <div class='item'>{{info.commit}}</div>
                </div>
             </form>
          </section>
           <section v-else-if="type=='del'" class='center'>
              <div>Are you sure you want to delete "{{info.name}}"?</div>
          </section>
          <footer class='footer'  v-if='type=="add"||type=="edit"'>
             <span @click='cancle'>Cancel</span>
             <div v-if='type=="add"' class='btn' @click='addEvent'>Add</div>
             <div v-else-if='type=="edit"' class='btn' @click='addEvent'>Save</div>
          </footer>
          <footer class='footer'  v-if='type=="del"'>
             <span @click='cancle'>Cancel</span>
             <div class='btn' @click='delEvent'>Delete</div>
          </footer>
           <footer class='footer'  v-else-if='type=="info"'>
             <div class='btn' @click='cancle'>OK</div>
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
        rating: '',
        commit: ''
      }
    }
  },
  mounted () {
    this.$refs.box.style.height = document.documentElement.clientHeight + 'px'
    if (this.type === 'edit') {
      this.add = this.info
    }
  },
  components: {
    Star
  },
  computed: {
    rating () {
      return this.add
    }
  },
  props: ['title', 'type', 'info'],
  methods: {
    addEvent () {
      this.$emit('add', this.add)
    },
    cancle () {
      this.$emit('cancle')
    },
    getLevel (val) {
      this.add.rating = val
    },
    delEvent () {
      this.$emit('del')
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


