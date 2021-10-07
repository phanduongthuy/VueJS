<template>
  <div class="container">
    <ProductForm class="productForm" @createProduct="create">
    </ProductForm>
    <ProductList class="productList" :products=products @deleteProduct="destroy">
    </ProductList>
  </div>
</template>

<script>
import ProductList from "./ProductList";
import ProductForm from "./ProductForm";
export default {
  name: "Exercise",
  components:{
    ProductForm,
    ProductList
  },
  data() {
    return{
      products: [],
      data: '',
    }
  },
  methods: {
    create(value){
      let today = new Date();
      let msp = '';
      msp = 'SP'+today.getTime();
      let data = {
            msp: msp,
            name: value[0].name,
            price: value[0].price,
            quantity: value[0].quantity
          }
      console.log(data)
      return this.products.push(data)
    },
    destroy(product){
      for (let i=0; i<this.products.length; i++){
        if (this.products[i].msp === product[0].msp){
          return this.products.splice(i, 1)
        }
      }
    }

  },
}
</script>

<style scoped lang="scss">
.container{
  padding: 50px;
  display: flex;
  justify-content: left;

  .productForm{
    width: 40%;
  }

  .productList{
    width: 60%;
  }

}
</style>