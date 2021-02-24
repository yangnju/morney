<template>
  <Layout class-prefix="layout">
    <NumberPad :value.sync="record.amount"/>
    <Types :value.sync="record.type"/>
    <notes @update:value="onUpdateNotes"/>
    <!--.sync 会接收组件对DataSource的修改-->
    <tags :data-source.sync="tags" @update:value="onUpdateTags"/>
  </Layout>
</template>

<script lang="ts">
import NumberPad from '@/components/money/NumberPad.vue';
import Types from '@/components/money/Types.vue';
import Notes from '@/components/money/Notes.vue';
import Tags from '@/components/money/Tags.vue';
import {Component} from 'vue-property-decorator';

type Record = {
  tags: string[]
  notes: string
  type: string
  amount: string
}
@Component({
  components: {Tags, Notes, Types, NumberPad}
})
export default class Money extends Vue {
  tags = ['衣', '食', '住', '行', '娱乐'];
  record: Record = {
    tags: [], notes: '', type: '-', amount: 0
  };

  onUpdateTags(value: string[]) {
    this.record.tags = value;
  }

  onUpdateNotes(value: string) {
    this.record.notes = value;
  }
}
</script>

<style lang="scss">
.layout-content {
  display: flex;
  flex-direction: column-reverse;
}
</style>