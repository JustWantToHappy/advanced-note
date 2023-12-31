## 组合式API
- setup函数版本
```html
<script >
  import {ref }from "vue"
  export default {
    setup(){
      const count=ref(0);
      const sb=ref({age:11});
      return {count,sb,increment:()=>{
        count.value++;
        sb.value.age++;
      }}
    }
  }
</script>

<template>
  <button @click="increment">Count is: {{ count }}</button>
  <div>{{sb.age}}</div>
</template>
```
- setup语法糖版本
`<script setup></script>`
```html
<script setup>
    import {ref} from "vue";
    const count=ref(0);
    function increment(){
        count.value++;
    }
</script>
<template>
    <button @click="increment"></button>
    <button @click="count++"></button>
</template>
```
## 选项式API
```html
<script>
export defualt {
    data:(){
        return {
            count:0;
        }
    },
    methods:{
        increment(){
            this.count++;
        }
    }
}
</script>