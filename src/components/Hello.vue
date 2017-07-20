<template>
  <div>
    <header class='header'>
      <img src="../assets/wp-logo2.png" alt=""> Welcome to Whinepad!
    </header>
    <section class='box'>
      <header class='boxTop'>
        <div class='add btn' @click='addActive=true'>+ add</div>
        <input type="text" class='search' placeholder="search" v-model='search'>
      </header>
      <table>
        <thead>
          <tr>
            <th class='name'>Name</th>
            <th class='year'>Year</th>
            <th class='grape'>Grape</th>
            <th class='rating'>Rating</th>
            <th class='action'>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for='(item,index) in Searchlist' :key='item'>
            <td class='name'>{{item.name}}</td>
            <td class='year'>{{item.year}}</td>
            <td class='grape'>{{item.grape}}</td>
            <td class='rating'>
              <Star :score='item.rating' disabled></Star>
            </td>
            <td>
              <div class='action'>
                 <span @click='handleInfo(item)'>查看</span>
                 <span @click='handleEdit(item,index)'>编辑</span>
                 <span @click='handleDel(item,index)'>删除</span>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </section>
    <AlertBox v-if='addActive' @add='handleAdd' @cancle='addActive=false' title='Add new item' type='add'></AlertBox>
    <AlertBox v-if='InfoActive'  @cancle='InfoActive=false' title='Item info' type='info' :info='info'></AlertBox>
    <AlertBox v-if='EditActive' @add='edit' @cancle='EditActive=false' title='Edit item' type='edit' :info='info'></AlertBox>
    <AlertBox v-if='DeleteActive' @del='del' @cancle='DeleteActive=false' title='Confirm deletion' type='del' :info='info'></AlertBox>
  </div>
</template>

<script>
import Star from './star.vue'
import AlertBox from './alertBxo.vue'
export default {
  name: 'hello',
  data () {
    return {
      addActive: false,
      InfoActive: false,
      EditActive: false,
      DeleteActive: false,
      info: {},
      list: [],
      index: '',
      search: ''
    }
  },
  mounted () {
    this.list = localStorage.getItem('list') ? JSON.parse(localStorage.getItem('list')) : []
  },
  computed: {
    Searchlist () {
      const key = this.search
      const shoppingList = this.list
      return shoppingList.filter(function (item) {
        // 此处fiter为javascript数组对象的一个方法，用于检测数值元素，并返回符合条件所有元素的数组
        return item.name.toLowerCase().indexOf(key.toLowerCase()) !== -1
      })
    }
  },
  components: {
    'Star': Star,
    'AlertBox': AlertBox
  },
  methods: {
    handleAdd (val) {
      this.list.push(val)
      this.addActive = false
      localStorage.setItem('list', JSON.stringify(this.list))
    },
    handleInfo (item) {
      this.info = item
      this.InfoActive = true
    },
    handleEdit (item, index) {
      this.info = item
      this.index = index
      this.EditActive = true
    },
    handleDel (item, index) {
      this.index = index
      this.info = item
      this.DeleteActive = true
    },
    edit (val) {
      this.list[this.index] = val
      console.log(this.list[this.index])
      localStorage.setItem('list', JSON.stringify(this.list))
      this.EditActive = false
    },
    del () {
      this.DeleteActive = false
      this.list.splice(this.index, 1)
      localStorage.setItem('list', JSON.stringify(this.list))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
  width: 100%;
  height: 120px;
  background: #6f001b;
  display: flex;
  align-items: center;
  color: #fff;
  font-family: Norican, cursive;
  padding: 20px;
  font-size: 50px;
}

.header img {
  margin-right: 20px;
}

.box {
  padding: 40px;
}

.boxTop {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.btn {
  width: 110px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: space-around;
  font-size: 20px;
  background: #6f001b;
  border-radius: 50px;
  color: #fff;
  font-weight: 700;
  font-size: 30px;
  padding: 0 10px;
  cursor: pointer;
}

.search {
  width: 200px;
  height: 40px;
  outline: none;
  padding: 10px;
}

table {
  width: 100%;
  margin-top: 20px;
}

table th {
  font-weight: normal;
  color: #7f7f7f;
  font-size: 13px;
  height: 30px;
}
table td{
  border-right:1px solid #F0F0F0; 
  background: #fff;
  padding:0 10px;
  height: 58px;
}
table td:last-child{
  border-right:none; 
}
thead .name {
  width: 15%;
}

thead .year {
  width: 10%;
}

thead .grape {
  width: 15%;
}

thead .rating {
  width: 25%;
}

thead .action {
  width: 35%;
}
tbody .name{
  font-weight: 700;
}
tbody .year{
   color: #7f7f7f;
   text-align: center;
}
tbody .grape{
  font-weight: 700;
  color: #6f001b;
}
</style>
