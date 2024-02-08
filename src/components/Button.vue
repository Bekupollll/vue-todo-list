<template>
  <button @click="onClick" class="btn" :style="{background: color}">{{text}}</button>
</template>

<script>
export default {
name:'button',
props:['text','color'],
methods:{
    onClick(){
      this.$emit('btnclick')
    }
}
}
</script>