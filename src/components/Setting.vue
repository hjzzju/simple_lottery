<template>
  <div class="setting">
    <h1>导入人员名单</h1>
    <div class="field is-grouped">
      <div class="control">
        <button class="button" @click="clear">清空抽奖历史</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import XLSX from 'xlsx'

export default {
  data () {
    return {
      content: ''
    }
  },
  methods: {
    clear () {
      localStorage.setItem('history', '')
      alert('已清空')
    }, 
  },
  created () {
    var url = "/staff.xlsx"  //放在public目录下的文件可以直接访问
    //读取二进制excel文件,参考https://github.com/SheetJS/js-xlsx#utility-functions
    axios.get(url, {responseType:'arraybuffer'})
    .then((res) => {
    var data = new Uint8Array(res.data)
    var wb = XLSX.read(data, {type:"array"})
    console.log(wb)
    const firstSheetName = wb.SheetNames[0]
    
    const first_worksheet = wb.Sheets[firstSheetName]
    const file_data = XLSX.utils.sheet_to_json(first_worksheet, { header: 1 })
    this.content = []
    for (var j = 0;j<file_data.length;j++){
      this.content.push(file_data[j][0])
    }
    localStorage.setItem('content', this.content)
    }).catch( err =>{
      this.err = err
    })
    // this.numbers = localStorage.getItem('numbers')
    // if (!this.numbers) {
    //   this.numbers = ['11', '22', '33', '44', '55', '66', '77', '88', '99'].join('\n')
    //   localStorage.setItem('numbers', this.numbers)
    // }
  }
}
</script>

<style scoped>
h1 {
  font-size: 30px;
  margin-bottom: 6px;
}

h2 {
  font-size: 20px;
  margin-bottom: 10px;
}

.setting {
  text-align: left;
  width: 50%;
}

.textarea {
  height: 300px;
}
</style>
