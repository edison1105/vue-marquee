# vue-marquee-list

> a marquee component for vue project

## Install

``` javascript
npm install vue-marquee-list
```

## How To Use

``` javascript
import ListMarquee from 'vue-marquee-list'
```
## Example

``` javascript
<template>
  <div id="app">
    <div class="marquee-container">
      <list-marquee :interval="1" :rowHeight="30" :rowCount="5">
        <div class="marquee-item" v-for="(item,i) in list" :key="i">
          <div>{{i}}______{{item}}</div>
        </div>
      </list-marquee>
    </div>
  </div>
</template>

<script>
import ListMarquee from 'vue-marquee-list'

export default {
  name: 'app',
  components: {
    'list-marquee':ListMarquee
  },
  data() {
    return {
      list: Array.from({length:10}).map(()=> '恭喜玩家一叶知秋获得五杀')
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.marquee-container{
  height:150px;
  overflow: hidden;
}
.marquee-item{
  height:30px;
  line-height: 30px;
}
</style>
```
