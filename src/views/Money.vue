<template>
  <Layout class-prefix="layout">
    <NumberPad/>
    <Types/>
    <Notes/>
    <Tags/>


  </Layout>
</template>

<script lang="ts">


  import NumberPad from '@/components/Money1/NumberPad.vue';
  import Tags from '@/components/Money1/Tags.vue';
  import Types from '@/components/Money1/Types.vue';
  import Notes from '@/components/Money1/Notes.vue';
  export default {
    name: 'Money',
    components: {Notes, Types, Tags, NumberPad},
  }
</script>

<style lang="scss">
.layout-content{

  display: flex;
  flex-direction: column-reverse;

}
</style>

