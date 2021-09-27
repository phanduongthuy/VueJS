<template>
  <div class="container">
    <div class="loginWrap">
      <div class="inputWrap">
        <div class="inputLabel">Tên đăng nhập</div>
        <input type="text" v-model="username">
      </div>
      <div class="inputWrap">
        <div class="inputLabel">Mật khẩu</div>
        <input type="password">
      </div>
      <button class="loginButton" @click="changeName">Đăng nhập</button>
    </div>
    <div class="infoWrap">
      <div class="infoLabel">
<!--        Xin chào {{ name }}-->
        Xin chào {{ username }}
<!--        Xin chào <span v-html="name"></span>-->
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  // props: {
  //   msg: String
  // }
  data(){
    return {
      // name: 'Phan Thùy',
      name: '<h1>Phan Thùy</h1>',
      username: 'thuypd',


    }
  },

  methods: {
    changeName() {
      this.name = 'Phan Dương Thùy'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 500px;

  .loginWrap {
    background: #f5f5f5;
    border: 1px solid #6e6e6e;
    padding: 24px;
    height: 250px;
    width: 300px;

    .inputWrap {
      margin-bottom: 12px;

      .inputLabel {
        font-weight: bold;
        margin-bottom: 8px;
        text-align: left;
    }

      input {
        width: 292px;
        height: 30px;
    }
  }

    button {
      width: 100%;
      height: 40px;
      border-radius: 5px;
      margin-top: 20px;
      background: #0080dd;
      color: #fff;
      border: unset;
      font-weight: bold;
      font-size: 16px;
      cursor: pointer;
  }
}

  .infoWrap {
    background: #fff;
    border: 1px solid #6e6e6e;
    padding: 24px;
    height: 250px;
    width: 250px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-left: 24px;

    .infoLabel {
      font-weight: bold;
      color: #00aaaa;
  }
}
}

</style>
