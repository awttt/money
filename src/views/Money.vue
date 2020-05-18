<template>
  <Layout class-prefix="layout">

    <NumberPad :value.sync="record.amount" @submit="saveRecord"/>
    <Types :value.sync="record.type"/>
    <div class="notes">
      <Notes field-name="备注"
             placeholder="在这里输入备注"
             @update:value="onUpdateNotes"/>
    </div>
    <Tags :data-source.sync="tags" @update:value="onUpdateTags"/>
  </Layout>
</template>

<script lang="ts">

  import Vue from 'vue';
  import NumberPad from '@/components/Money1/NumberPad.vue';
  import Tags from '@/components/Money1/Tags.vue';
  import Types from '@/components/Money1/Types.vue';
  import FormItem from '@/components/Money1/FormItem.vue';
  import {Component, Model, Watch} from 'vue-property-decorator';
  import recordListModel from '@/models/recordListModel';
  import store from '@/store/index2';


  const recordList = recordListModel.fetch();


  @Component({components: {Notes: FormItem, Types, Tags, NumberPad},})
  export default class Money extends Vue {
    tags = store.tagList;
    recordList = store.recordList;
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
      store.createRecord(this.record);
    }
  }
</script>

<style lang="scss">
  .layout-content {
    display: flex;
    flex-direction: column-reverse;
  }

  .notes {
    padding: 2px 0;
  }

</style>

