<template>
  <div class="productForm">
    <h3>Sản phẩm</h3>
    <div class="inputWrap">
      <div class="inputLabel">Tên sản phẩm<span>(*)</span></div>
      <input type="text" v-model="data.name" placeholder="Nhập tên sản phẩm">
      <span class="error" v-if="data.errName">Tên sản phẩm không được để trống</span>
    </div>
    <div class="inputWrap">
      <div class="inputLabel">Đơn giá<span>(*)</span></div>
      <input type="number" v-model="data.price" placeholder="Nhập đơn giá sản phẩm">
      <span class="error" v-if="data.errPrice">Giá sản phẩm không được để trống</span>
    </div>
    <div class="inputWrap">
      <div class="inputLabel">Số lượng<span>(*)</span></div>
      <input type="number" v-model="data.quantity" placeholder="Nhập số lượng sản phẩm">
      <span class="error" v-if="data.errQuantity">Số lượng sản phẩm không được để trống</span>
    </div>
    <div class="btn">
      <button class="btn-create" @click="store()">Tạo mới</button>
      <button class="btn-cancel" @click="cancel()">Huỷ</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['product'],
  data() {
    return {
      data: 
        {
          name: '',
          price: '',
          quantity: '',
          errName: false,
          errPrice: false,
          errQuantity: false
        }
    }
  },
  methods: {
    validate(name, price, quantity) {
      if(name === "") {
        this.data.errName = true
      }else {
        this.data.errName = false
      }
      if(price === "") {
        this.data.errPrice = true
      }else {
        this.data.errPrice = false
      }
      if(quantity === "") {
        this.data.errQuantity = true
      }else {
        this.data.errQuantity = false
      }
      return [
          this.data.errName,
          this.data.errPrice,
          this.data.errQuantity
      ]
    },
    store() {
      let name = this.data.name
      let price = this.data.price
      let quantity = this.data.quantity
      let errName = this.data.errName
      let errPrice = this.data.errPrice
      let errQuantity = this.data.errQuantity
      this.validate(name, price, quantity)
      if(errName && errPrice &&  errQuantity){
        console.log(errName, errPrice, errQuantity)
      }else {
        let product = []
        product['name'] = name
        product['price'] = price
        product['quantity'] = quantity
        this.$emit('createProduct', [product])
        return[
          this.data.name = '',
          this.data.price = '',
          this.data.quantity = '',
          this.data.errName = false,
          this.data.errPrice = false,
          this.data.errQuantity = false
        ]
      }

    },

    cancel(){
      return[
        this.data.name = '',
        this.data.price = '',
        this.data.quantity = '',
        this.data.errName = false,
        this.data.errPrice = false,
        this.data.errQuantity = false
      ]
    },

  },
  watch: {

  }
}
</script>
<style scoped lang="scss">
.productForm{
  border: 2px solid #f2f4f8;
  padding: 20px;
  margin-right: 30px;

  h3{
    color: #0080dd;
  }

  .inputWrap{
    padding: 10px;
    text-align: left;

    .error{
      color: red;
    }

    .inputLabel{
      font-weight: bold;
      text-align: left;
      span{
        color: red;
      }
    }
    input{
      width: 100%;
      height: 30px;
      border: 2px solid #f2f4f8;
      border-radius: 5px;
    }
  }

  .btn{
    float: right;

    button{
      height: 30px;
      width: 80px;
      margin: 5px;
      font-weight: bold;
      border: none;
      border-radius: 5px;
    }
    button:hover{
      opacity: 0.5;
      cursor: pointer;
    }

    .btn-create{
      color: white;
      background-color: #0080dd;
    }

    .btn-cancel{
      background-color: #d8e0ea;
    }

  }
}
</style>