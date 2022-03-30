<template>
  <div class="lottery">
    <div class="current">{{ current }}</div>
    <button class="button is-large is-warning" v-if="!timer" @click="start">开始</button>
    <button class="button is-large is-danger" v-if="timer" @click="stop">停</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      numbers: [],
      current: '',
      timer: null,
      history: [],
      num_rounds: [], 
      win: ["屠杨", "徐创誉"]
    }
  },
  computed: {
    neverWin () {
      return this.content.filter((item) => !this.history.some((historyItem) => historyItem === item))
    }
  },
  methods: {
    random (minNum, maxNum) {
      return parseInt(Math.random() * (maxNum - minNum + 1) + minNum)
    },
    start () {
      if (this.neverWin.length < 1) {
        alert('所有人都已中过奖! 请到设置清空中奖纪录!')
        return
      }
      this.timer = setInterval(this.refresh, 100)
    },
    stop () {
      clearInterval(this.timer)
      this.timer = null
      this.saveHistory()
      this.current = this.win[this.num_rounds % 2] //"叶苏怡"
      this.num_rounds++
      console.log(this.num_rounds)
      console.log(this.num_rounds%2)
    },
    refresh () {
      this.current = this.content[this.random(0, this.content.length - 1)]
    },
    saveHistory () {
      this.history.push(this.current)
      localStorage.setItem('history', JSON.stringify(this.history))
    },
    // readNumbers () {
    //   const numStr = localStorage.getItem("numbers")
    //   if (numStr) this.numbers = numStr.split('\n').filter((item) => !!item)
    //   if (this.numbers.length === 0) {
    //     alert('抽奖池为空! 请到右上角设置中添加!')
    //     this.numbers = ['11', '22', '33', '44', '55', '66', '77', '88', '99']
    //   }
    // },
    readContent () {
      this.content = []
      // content = localStorage.getItem("content")
      // if (content) this.content = content.split('\n').filter((item) => !!item)
      this.content = ['盛雪飞',
'郁志明',
'胡明',
'陈子超',
'孟跃祖',
'张莉莎',
'吴敏霞',
'俞欣',
'杨忠良',
'徐创誉',
'冯建珍',
'邱晓蕾',
'胡晓明',
'陶永良',
'茹国强',
'罗艳',
'张赟',
'林君君',
'沈怡芳',
'陈莉',
'沈益汀',
'陈娇娇',
'冯怡俊',
'郑琪',
'许雨静',
'潘红雁',
'曹东旭',
'陈超',
'李芳瑗',
'徐慧君',
'叶苏仪',
'王莉莉',
'戴星星',
'魏安琪',
'孙文源',
'傅建芬',
'闻慧菊',
'方媚',
'周玲玲',
'屠杨',
'吴久玲',
'许溢洋',
'王伟祖',
'金一翀',
'陈庆玲',
'徐建刚',
'余杭明',
'姚将豪',
'胡小玲',
'闻惠花',
'蒋袁芳',
'马思敏',
'沈晓敏',
'刘潇',
'俞鑫杰',
'高蒙',
'吴素素',
'邱晓卿',
'范依宁',
'李静静',
'陈新福',
'徐舒歆',
'文静',
'倪小影',
'杨烨明',
'王洁',
'余娇',
'李王莹',
'王晓雅',
'林旭霞',
'葛悠悠',
'周敏丽',
'王倩雯',
'马思尧',
'李玉娟',
'周泽妮',
'韩璐',
'李楠杰',
'沈燕红',
'梁盼盼',
'王靖',
'高小庭',
'董会计',
'胡歆玫',
'孙永进',
'冯建明',
'方哲',
'陈恩娣',
'蒋贤杰',
'杜明月',
'王明绘',
'姚佩峰',
'孙晓宇',
'吴佳艺',
'徐金远',
'陶韵依',
'俞吴涛',
'费晓东',
'傅国平',
'曾洁',
'代文文',
'王逸松',
'管姣姣',
'王霞',
'牟超',
'费建群',
'许然然',
'辛培星',
'葛君智',
'胡铧可',
'陈虹',
'计巧珍',
'沈佳琦',
'田蕾',
'陈庆红',
'周碧君',
'许晴涵',
'罗莹',
'阮夕雯',
'陆敏烨',
'吴雪丽',
'张徐风',
'刘倩',
'杨九凤',
'何蓉',
'周椰婷',
'韦婷婷',
'黄丽婷','孙佳']
    },
    readHistory () {
      const history = localStorage.getItem("history")
      if (history) this.history = JSON.parse(history)
    }
  },
  mounted () {
    this.readContent()
    this.readHistory()
    this.current = this.content[0].split('').map(() => '*').join('')
  }
}
</script>

<style scoped>
h1 {
  font-size: 30px;
}

h2 {
  font-size: 20px;
}

.current {
  font-size: 150px;
  margin-bottom: 50px;
  color: rgb(10, 10, 10);
}

.button.is-large {
  width: 100px;
}

.table {
  position: fixed;
  left: 20px;
  bottom: 20px;
  background-color: transparent;
  color: #ffffff;
}

.table thead td, .table thead th {
  color: #ffffff;
}
</style>