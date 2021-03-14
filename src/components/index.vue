<template>
  <div>
    <!-- <el-button type="primary" @click="list">取得資料</el-button>
    <el-button type="primary" @click="checkIfLoading">查看</el-button> -->
    <el-table
      :data="tableData"
      style="width: 100%"
      class="data-table">
      <el-table-column
        prop="name"
        label="姓名"
        width="180">
      </el-table-column>
      <el-table-column
        prop="age"
        label="年齡">
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import mock from '../mock';
import axios from 'axios';

export default {
  data () {
    return {
      tableData: [
          {
            name: '宮本武藏',
            age:20
          },
          {
            name: '李逍遙',
            age:15
          },
          {
            name: 'Jack',
            age:10
          },
          {
            name: 'Shang',
            age:11
          },
          {
            name: 'Jeff',
            age:12
          },
          {
            name: 'Lisa',
            age:12
          },
          {
            name: 'JE',
            age:55
          },
          {
            name: 'RD',
            age:12
          },
          {
            name: 'JR',
            age:12
          },
        ],
    }
  },
  methods:{
    list() {
        console.log('載入');
        axios.post("/list").then(response => {
            if (response.data) {
                // console.log(response.data)
                // alert(response.data.name + ',' + response.data.age)
                this.tableData.push({
                  name: response.data.name,
                  age: response.data.age,
                })
            }
        })
    },
    checkIfLoading (){
      console.log('成功滾動偵測');
      var scrollTop = document.querySelector('.data-table').scrollTop;
      var innerHeight = document.querySelector(".el-table__row").offsetHeight*this.tableData.length;
      var viewHeight = document.querySelector(".data-table").offsetHeight;
      // var hideScrollHeight = innerHeight-viewHeight;
      // var contentHeight =innerHeight+scrollTop ;
      

        console.log(document.querySelector('.data-table'), scrollTop, innerHeight-viewHeight);
        if ( scrollTop >= innerHeight-viewHeight &&  innerHeight-viewHeight >= 0) {
          this.list();
        }
        
    },
    scrollHandler(){
      var table = document.querySelector('.data-table');
      table.addEventListener('scroll', this.checkIfLoading);
    }
  },
  mounted(){
    // this.checkIfLoading();
    this.scrollHandler();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.data-table {
  max-height: 400px;
  overflow: scroll;
}
</style>
