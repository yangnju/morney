<template>
  <layout>
    <Icon name="left"/>
    <span>编辑标签</span>
    <Notes field-name="标签名" placeholder="请输入标签名"/>
  </layout>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component} from 'vue-property-decorator';
import tagListModel2 from '@/models/tagListModel2';
import Notes from '@/components/money/Notes.vue';

@Component({
  components: {Notes}
})
export default class EditLabel extends Vue {
  create() {
    const id = this.$route.params.id;
    tagListModel2.fetch();
    const tags = tagListModel2.data;
    const tag = tags.filter(t => t.id === id)[0];
    if (tag) {
      console.log(tag);
    } else {
      this.$router.replace('/404');
    }
  }
}
</script>

<style lang="scss" scoped>

</style>