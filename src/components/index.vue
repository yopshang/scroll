<template>
  <div>
    <el-button type="primary" @click="list">取得資料</el-button>
    <el-table
      :data="tableData"
      style="width: 100%">
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
            name: '王小虎',
            age:0
          },
        ]
    }
  },
  methods:{
    list() {
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
    }
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
</style>
