<template>
    <div>
      <v-dialog
          v-model="dialog"
          max-width="650px"
      >
          <v-card>
              <v-card-title>
                  <span>Thêm mới loại sản phẩm</span>
              </v-card-title>
          <v-card-text>
              <v-form>
                  <v-container>
                      <v-row>
                          <v-col>
                              <v-text-field
                                  label="Tên loại sản phẩm"
                                  v-model="data.categoryName"
                              >
                              </v-text-field>
                          </v-col>
                      </v-row>
                  </v-container>
              </v-form>
          </v-card-text>
          <v-card-actions>
              <v-space></v-space>
              <v-btn class="mr-2" color="gey" @click="this.$emit('close')">Hủy</v-btn>
              <v-btn class="mr-2" color="blue" @click="addCategory">Lưu</v-btn>
          </v-card-actions>
          </v-card>
      </v-dialog>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  export default {
      name: 'AddView',
      data(){
        return{
            data:{
                categoryName:''
            }
        }
      },
      methods: {
        addCategory() {
            axios.post("https://652a52484791d884f1fcc90c.mockapi.io/tranquanganh-deso1/quanh", this.data)
            .then(response => {
                this.$emit('close');
                this.$emit('updateData');
                console.log(response.status);
      })
            .catch(error => {
                console.log(error);
      });
  }
},
      props: ['dialogAdd'],
      computed:{
          dialog:{
              get(){
              return this.dialogAdd
          },
              set(value) {
                  if(!value) {
                      this.$emit('close');
                  }
              }
          }
      }
  }
  </script>
  
  <style>
  
  </style>
