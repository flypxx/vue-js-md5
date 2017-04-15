<template>
  <div class="hello">
    <div class="table">
      <div class="row-wrapper">
        <div class="name">name</div>
        <div class="func">function</div>
        <div class="value">value</div>
      </div>
      <div class="row-wrapper">
        <div class="name">hello</div>
        <div class="func">md5('hello')</div>
        <div class="value">{{md5Str}}</div>
      </div>
      <div class="row-wrapper">
        <div class="name">123</div>
        <div class="func">md5(123)</div>
        <div class="value">{{md5Num}}</div>
      </div>
      <div class="row-wrapper">
        <div class="name">{id: '20170415',name: 'movie',lang: 'English',price: '80'}</div>
        <div class="func">md5(getSig(obj))</div>
        <div class="value">{{md5Json}}</div>
      </div>
    </div>
  </div>
</template>

<script>
import md5 from 'js-md5'
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      flagid: 'ef4bfb57749acc663f0b1e52e097945f'
    }
  },
  computed: {
    md5Str () {
      return md5('hello')
    },
    md5Num () {
      return md5(123)
    },
    md5Json () {
      let obj = {
        id: '20170415',
        name: 'movie',
        lang: 'English',
        price: '80'
      }
      return md5(this.getSig(obj))
    }
  },
  methods: {
    getSig (data) {
      let keyArr = []
      let valArr = []
      for (var key in data) {
        keyArr.push(key)
      }
      keyArr = keyArr.sort()
      keyArr.forEach((item) => {
        if (typeof (data[item]) !== 'undefined') {
          valArr.push(item + data[item])
        }
      })
      let str = valArr.join('') + this.flagid
      return md5(str)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  padding: 20px;
}
.table {
  line-height: 40px;
  border: 1px solid #efefef;
}
.row-wrapper {
  display: flex;
  height: 40px;
  text-align: center;
}
.row-wrapper:first-child {
  border-bottom: 1px solid #f3f5f7;
}
.name, .func {
  flex: 0 0 33%;
}
.value {
  flex: 0 0 34%;
}
</style>
