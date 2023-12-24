<template>
    <div class="product-list-container">
      <v-row class="product-list-header">
        <v-icon>mdi-home</v-icon>
        <h3>Danh sách loại sản phẩm</h3>
        <v-spacer></v-spacer>
        <v-btn icon size="small" class="add-product-btn">
          <v-icon>mdi-plus</v-icon>
        </v-btn>
      </v-row>
      <v-row>
        <v-col>
          <v-card class="product-list-card">
            <v-table class="product-list-table">
              <!-- Table Head -->
              <thead>
                <tr>
                  <th>STT</th>
                  <th>Mã loại SP</th>
                  <th>Tên loại SP</th>
                  <th>Chức năng</th>
                </tr>
              </thead>
              <!-- Table Body -->
              <tbody>
                <tr v-for="(item,index) in categories" :key="index">
                  <td>{{ index+1 }}</td>
                  <td>{{ item.categoryId }}</td>
                  <td>{{ item.categoryName }}</td>
                  <td class="function-buttons">
                    <v-btn color="blue" size="x-small" icon>
                      <v-icon>mdi-pencil</v-icon>
                    </v-btn>
                    <v-btn color="red" size="x-small" icon>
                      <v-icon>mdi-delete</v-icon>
                    </v-btn>
                  </td>
                </tr>
              </tbody>
            </v-table>
          </v-card>
        </v-col>
      </v-row>
      <!-- Add, Edit, Delete Dialogs -->
      <add-view-dialog />
      <edit-view-dialog />
      <delete-confirmation-dialog />
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  export default {
      name:'EditView',
      data(){
          return{
              data:{
                  categoryId:'',
                  categoryName:'',
              }
          }
      },
      methods:{
          updateCategory(){
            axios.post("https://652a52484791d884f1fcc90c.mockapi.io/tranquanganh-deso1/quanh/"+this.data.categoryId, this.data)
              .then(response=>{
                  this.$emit('close');
                  this.$emit('updateData')
                  console.log(response.status);
              })
              .catch(error =>{
                  console.log(error);
              })
          }
      },
      props: [`dialogEdit`,'currentItem'],
        computed:{
            dialog:{
                get(){
                return this.dialogEdit;
            },
            set(value){
                if(!value){
                    this.$emit(`close`);
                }
            }
          }
      },
      watch:{
          currentItem:function(){
              this.data.categoryID = this.currentItem.categoryID;
              this.data.categoryName = this.currentItem.categoryName;
          }
      }
  }
  </script>
  
  <style scoped>
.product-list-container {
  /* Add your styles here */
}

.product-list-header {
  /* Add your styles here */
}

.add-product-btn {
  /* Add your styles here */
}

.product-list-card {
  /* Add your styles here */
}

.product-list-table {
  /* Add your styles here */
}

.function-buttons {
  /* Add your styles here */
}

/* Add responsive design styles */
@media (max-width: 600px) {
  /* Add your mobile styles here */
}
</style>