<template>
  <Layout class-prefix="layout">
    {{record}}
    <NumberPad :value.sync="record.amount" @submit="saveRecord"/>
    <Types :value.sync="record.type"/>
    <Notes @update:value="onUpdateNotes"/>
    <Tags :data-source.sync="tags" @update:value="onUpdateTags"/>
  </Layout>
</template>

<script lang="ts">

  import Vue from 'vue';
  import NumberPad from '@/components/Money1/NumberPad.vue';
  import Tags from '@/components/Money1/Tags.vue';
  import Types from '@/components/Money1/Types.vue';
  import Notes from '@/components/Money1/Notes.vue';
  import {Component, Model, Watch} from 'vue-property-decorator';
  import model from '@/model';

  const recordList = model.fetch();

  @Component({components: {Notes, Types, Tags, NumberPad},})
  export default class Money extends Vue {
    tags = ['衣', '食', '住', '行'];
    recordList: RecordItem[] = recordList;
    record: RecordItem = {
      tags: [], notes: '', type: '-', amount: 0
    };



    onUpdateTags(value: string[]) {
      this.record.tags = value;
    }

    onUpdateNotes(value: string) {
      this.record.notes = value;
    }

    onUpdateAmount(value: string) {
      this.record.amount = parseFloat(value);
    }

    saveRecord(value: string) {
      const record2: RecordItem= model.colone(this.record);
      record2.createdAt= new Date()
      this.recordList.push(record2);
    }

    @Watch('recordList')
    onRecordListChange() {
      model.save(this.recordList)
    }
  }
</script>

<style lang="scss">
  .layout-content {
    display: flex;
    flex-direction: column-reverse;
  }
</style>

