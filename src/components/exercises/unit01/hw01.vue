<template>
  <div class="container">
    <div class="loginWrap">
      <div class="inputWrap">
        <div class="inputLabel">Nhập tiêu đề</div>
        <input type="text" name="title" v-model="title">
      </div>
      <div class="inputWrap">
        <div class="inputLabel">Nhập nội dung</div>
        <textarea name="content" id="" v-model="content"></textarea>
      </div>
    </div>
    <div class="infoWrap">
      <div class="infoLabel">
        <h3>{{title}}</h3>
        <p v-html="content"></p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      title: 'Zent Coding School',
      content: 'Happy class',
    }
  },
  methods: {

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  @import "../../../assets/scss/Unit01/hw01";
</style>
