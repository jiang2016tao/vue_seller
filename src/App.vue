<template>
  <div >
    <div class="header">
      header
    </div>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评价</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <div class="body-content">
      <router-view/>
    </div>
    <!--<router-view/>-->
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
  .tab{
    display: flex;
    height: 40px;
    line-height: 40px;
    border-bottom: 1px solid #eeeeee;
  }
  .tab-item{
    flex: 1;
    text-align: center;
  }
  .tab-item a{
    text-decoration: none;
    display: block;
  }
  .tab-item a.router-link-active{
    color: red;
  }
</style>
