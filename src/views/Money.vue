<template>
  <Layout class-prefix="layout">

    <NumberPad :value.sync="record.amount" @submit="saveRecord"/>

    <Tabs :data-source="recordTypeList"
          :value.sync="record.type"/>
    <div class="notes">
      <Notes field-name="备注"
             placeholder="在这里输入备注"
             @update:value="onUpdateNotes"/>
    </div>
    <Tags />
  </Layout>
</template>

<script lang="ts">

  import Vue from 'vue';
  import NumberPad from '@/components/Money1/NumberPad.vue';
  import Tags from '@/components/Money1/Tags.vue';
  import FormItem from '@/components/Money1/FormItem.vue';
  import {Component} from 'vue-property-decorator';
  import recordTypeList from '@/constant/recordTypeList';
  import Tabs from '@/components/Tabs.vue';





  @Component(
    {components: {Notes: FormItem,Tags, NumberPad,Tabs},

    })
  export default class Money extends Vue {

    get(){
      return this.$store.state.recordList
    }

    recordTypeList = recordTypeList

    record: RecordItem = {
      tags: [], notes: '', type: '-', amount: 0
    };

    created(){
      this.$store.commit('fetchRecords')
    }


    onUpdateNotes(value: string) {
      this.record.notes = value;
    }

    onUpdateAmount(value: string) {
      this.record.amount = parseFloat(value);
    }

    saveRecord(value: string) {
      this.$store.commit('createRecord',this.record)
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

