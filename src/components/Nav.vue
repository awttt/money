<template>
    <div>
        <div>
      <router-link to='/money'>
      <svg>
          <use xlink:href="icon_label"/>
      </svg>
      计账</router-link>|
      <router-link to='/labels'>标签</router-link>|
      <router-link to='/statistics'>统计</router-link>
    </div>
    </div>
</template>

<script lang="ts">
import x from '@/assets/icons/icon_label.svg'
console.log(x);
    export default{
        name:'Nav'
    }
</script>

<style scoped>

</style>