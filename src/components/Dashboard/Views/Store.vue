<template>
<!DOCTYPE html>
<html lang="en">
<head>
 <meta charset="utf-8">
 <meta name="viewport" content="width=device-width, initial-scale=1">
 <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">

</head>
<body>
  <form style="background-color:#f4f3ef">
    <label ><font size="4">Create Product</font></label>
  <div class="form-group">
    <label for="inputsm">Name</label>
    <input class="form-control input-sm" id="name" type="text" v-model="product.name">
  </div>
   <div class="form-group">
    <label for="inputsm">($)Price</label>
    <input class="form-control input-sm" id="price" type="number" v-model="product.price">
  </div>
  <div class="form-group">
    <label for="inputsm">SellerName</label>
    <input class="form-control input-sm" id="seller" type="text" v-model="product.seller">
  </div>
  <div> <button type="button" @click="add()" class="btn btn-primary btn-lg btn-block">Create</button> </div>
</form>
<div><label ><font size="4">Edit Product</font></label></div>
<div><label for="inputsm1">Name</label>
<input class="form-control input-sm" id="namee" type="text" v-model="product.name"></div>
<div><label for="inputsm">($)Price</label>
 <input class="form-control input-sm" id="price" type="number" v-model="product.price">
</div>
<div class="table-responsive" style="background-color:#f4f3ef">
 <h2 style="background-color:#f4f3ef" >Products</h2>
 <table class="table table-striped table-bordered" style="background-color:#E6E6FA">
   <thead>
     <tr style="background-color:gold">
       <th width="5%">ID</th>
       <th width="10%">Name</th>
       <th width="10%">Price</th>
       <th width="10%">Created at</th>
       <th width="10%">Updated at</th>
       <th width="15%">Seller Name</th>
       <th width="15%"><i class="fa fa-wrench"></i></th>

     </tr>
   </thead>
   <tbody>
     <tr v-for="productprod in products.data">
        <td class="text-left">{{ productprod._id}}</td>
        <td class="text-left">{{ productprod.name}}</td>
        <td class="text-left">{{ productprod.price}}</td>
        <td class="text-left">{{ productprod.createdAt}}</td>
        <td class="text-left">{{ productprod.updatedAt}}</td>
        <td class="text-left">{{ productprod.seller}}</td>
        <td>
        <button type="button"  @click="deletep(productprod._id)" class="btn btn-info" ><span class="fa fa-trash"></span></button>
      </button>
   <button type="button" @click="editproduct(productprod._id)" class="btn btn-info">
<span class="fa fa-edit"></span>
</button>
<button type="button"  class="btn btn-info">
<span class="fa fa-search"></span>
</button>
        </td>
     </tr>
   </tbody>
 </table>
</div>

</body>
</html>
</template>
<script>
/* eslint-disable */
import axios from 'axios';
export default {
    name:'product',
    data() {
        return {
            products: [],
            editp: [],
              product: {
              name: '',
              price: '',
              seller: ''
            }
          }
    },
    created (){
      this.view();
    },
    methods: {
      add () {
        let newProduct = {
          name: this.product.name,
          price: this.product.price,
          seller: this.product.seller
        }
        console.log(newProduct)
        axios.post('http://localhost:3000/api/product/createProduct', newProduct)
          .then((response) => {
            console.log(response)
        })
        .catch((error) => {
          console.log(error)
        })
        window.location.reload()
    },
    view () {
      var k= this
      axios.get('http://localhost:3000/api/product/getProducts')
      .then((response) => {
        this.products = response.data
        console.log(response.data)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    deletep(Id) {
      axios.delete('http://localhost:3000/api/product/deleteProduct/' + Id)
      .then((response) => {
        this.products.splice(index, 1)
      })
      .catch((error) => {
        console.log(error)
      })
      window.location.reload()
    },
    editproduct(Id) {
      let editProduct= {
        name: this.editproduct.name,
        price: this.editproduct.price
      }
      console.log(Id)
        axios.patch('http://localhost:3000/api/product/updateProduct/'+ Id, editProduct)
        .then((response) => {
          console.log(response)
      })
      .catch((error) => {
        console.log(error)
      })
      }
  }
}
</script>
