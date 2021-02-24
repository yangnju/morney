<template>
  <Layout class-prefix="layout">
    <NumberPad/>
    <Types/>
    <notes/>
    <!--.sync 会接收组件对DataSource的修改-->
    <tags :data-source.sync="tags"/>
  </Layout>
</template>

<script lang="ts">
import NumberPad from "@/components/money/NumberPad.vue";
import Types from "@/components/money/Types.vue";
import Notes from "@/components/money/Notes.vue";
import Tags from "@/components/money/Tags.vue";
export default {
  name: 'Money',
  components: {Tags, Notes, Types, NumberPad},
  data(){
    return{
      tags: ['衣','食','住','行','娱乐']
    }
  }
};
</script>

<style lang="scss">
.layout-content {
  display: flex;
  flex-direction: column-reverse;
}
</style>