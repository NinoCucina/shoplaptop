<template>
    <div>
        <v-dialog v-model="dialog"
         max-width="640px">
            <v-card>
                <v-card-tittle>
                    <span>Cập nhật loại sản phẩm</span>
                </v-card-tittle>
                <v-card-text>
                    <v-form>
                        <v-container>
                            <v-row>
                                <v-col>
                                    <v-text-field
                                    label="Tên loại sản phẩm"
                                    v-model="data.categoryName"
                                    ></v-text-field>
                                </v-col>
                            </v-row>
                        </v-container>
                    </v-form>
                </v-card-text>
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn
                        class="mr-2" 
                        color="grey darken-3"
                        @click="this.$emit(`close`)"
                    >Hủy</v-btn>
                    <v-btn
                    color="primary"
                    @click="updateCategory">Cập nhật</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
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
  
  <style>
  
  </style>