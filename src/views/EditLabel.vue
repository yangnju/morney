<template>
  <layout>
    编辑标签
  </layout>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component} from 'vue-property-decorator';
import tagListModel2 from '@/models/tagListModel2';
@Component
export default class EditLabel extends Vue {
  create(){
    const id = this.$route.params.id
    tagListModel2.fetch()
    const tags = tagListModel2.data
    const tag = tags.filter(t => t.id === id)[0]
    if (tag){
      console.log(tag)
    } else {
      this.$router.replace('/404')
    }
  }
}
</script>

<style lang="scss" scoped>

</style>