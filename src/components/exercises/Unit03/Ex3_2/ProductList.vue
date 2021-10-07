<template>
  <div class="productList">
    <table class="table">
      <tr class="title">
        <th>Mã sản phẩm</th>
        <th>Tên sản phẩm</th>
        <th>Giá sản phẩm</th>
        <th>Số lượng</th>
        <th>Trạng thái</th>
        <th>Hành động</th>
      </tr>
      <tr class="products" v-for="product in data" :key="product.msp">
        <td>{{product.msp}}</td>
        <td>{{product.name}}</td>
        <td>{{product.price | formatPrice }}</td>
        <td>{{product.quantity}}</td>
        <td v-if="product.quantity > 0" class="statusStock">Còn hàng</td>
        <td v-else class="statusOutStock">Hết hàng</td>
        <td>
          <button class="btn btn-edit" @click="edit(product)">Sửa</button>
          <button class="btn btn-del" @click="destroy(product)">Xoá</button>
        </td>
      </tr>
      <tr>
        <td class="product-null" colspan="6"  v-if="products.length === 0">Không có dữ liệu</td>
      </tr>
    </table>
    <div class="pagination">
      <span>Hiển thị {{a}} - {{b}} trên tổng {{c}} (trang {{d}})</span>
      <div class="pagination-group">
        <el-button class="pagination-btn" @click="prev" :disabled="prevDisabled" icon="el-icon-arrow-left" ></el-button>
        <el-button class="pagination-btn" @click="next" :disabled="nextDisabled" icon="el-icon-arrow-right" ></el-button>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  props: ['products'],
  name: "ProductList",
  data() {
    return {
      data: this.products,
      a: 0,
      b: 0,
      c: 0,
      d: 0,
      prevDisabled: true,
      nextDisabled: true,
    }
  },
  filters: {
    formatPrice (value) {
      return new Intl.NumberFormat('vi-VN', { style: 'currency', currency: 'VND' }).format(value);
    },
  },
  methods: {

    destroy(product){
      this.$emit('deleteProduct', [product])
      this.data = this.products.slice(this.a-1, this.b);
    },

    prev(){
      if(this.a >= 5){
        this.a-=5;
        this.d-=1;
        this.prevDisabled = false
      }else {
        this.prevDisabled = true
      }
      if (this.b === this.products.length){
        let count = this.b%5;
        console.log(count)
        this.b-=count;
      }else {
        this.b-=5;
      }
    },

    next(){
      this.a+=5;
      if (this.b+5 > this.products.length){
        let count = this.products.length - this.b;
        this.b+=count;
      }else {
        this.b+=5;
      }
      this.d+=1;
    }
  },
  

  watch: {


  }
}
</script>

<style scoped lang="scss">
.productList{
  .table{
    border: 1px solid #f2f4f8;
    width: 100%;

    .title{
      background-color: #f2f6fe;
      height: 40px;
    }

    .products{
      td{
        padding: 5px 10px;
      }
    }

    .btn{
      height: 30px;
      width: 50px;
      text-align: center;
      margin: 5px;
      border: none;
      border-radius: 5px;
      font-weight: bold;
      color: white;
    }

    .btn-edit{
      background-color: orange;
    }
    .btn-del{
      background-color: red;
    }

    .product-null{
      text-align: center;
      padding: 10px;
    }

    .statusOutStock{
      color: red;
    }
    .statusStock{
      color: blue;
    }
  }

  .pagination{
    margin-top: 20px;
    .pagination-group{
      float: right;
      .pagination-btn{
        padding: 5px;
      }
    }
  }
}
</style>