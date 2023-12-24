<template>
  <v-app :style="{ background: $vuetify.theme.themes.dark.background }">
    <side-bar-admin :drawer="drawer" />
    <div class="admin-content">
      <v-row class="header-row">
        <h3 class="header-title">Danh sách loại sản phẩm</h3>
        <v-spacer></v-spacer>
        <v-btn icon size="large" class="add-btn" @click="dialogAdd = true">
          <v-icon large>mdi-plus</v-icon>
        </v-btn>
      </v-row>
      <v-row>
        <v-col>
          <v-card class="data-card">
            <v-table dense striped>
              <thead>
                <tr>
                  <th>STT</th>
                  <th>Mã loại SP</th>
                  <th>Tên loại SP</th>
                  <th>Chức năng</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(item, index) in categories" :key="index">
                  <td>{{ index + 1 }}</td>
                  <td>{{ item.categoryId }}</td>
                  <td>{{ item.categoryName }}</td>
                  <td>
                    <v-btn color="info" class="mr-2" fab small dark @click="dialogEdit = true, currentItem = item">
                      <v-icon>mdi-pencil</v-icon>
                    </v-btn>
                    <v-btn color="error" fab small dark @click="dialogDelete = true, categoryId = item.categoryId">
                      <v-icon>mdi-delete</v-icon>
                    </v-btn>
                  </td>
                </tr>
              </tbody>
            </v-table>
          </v-card>
        </v-col>
      </v-row>
      <add-view
        :dialogAdd = "dialogAdd"
        @close="dialogAdd = false"
        @updateData = "getCategories"
      />
      <edit-view
        :dialogEdit = "dialogEdit"
        :currentItem = "currentItem"
        @close="dialogEdit = false"
        @updateData = "getCategories"
      />
    <v-dialog max-width="450px" v-model="dialogDelete">
      <v-card>
          <v-alert type="error">
              <v-row align="center">
                  <v-col cols="11" class="text-center">
                      Bạn có đồng ý xóa không
                  </v-col>
              </v-row>
              <v-row align="center">
                  <v-spacer></v-spacer>
                  <v-col cols="5">
                      <v-btn variant="text" @click="deleteCategory">Đồng ý</v-btn>
                  </v-col>
                  <v-col cols="6">
                      <v-btn variant="text" @click="dialogDelete=false">Hủy bỏ</v-btn>
                  </v-col>
              </v-row>
          </v-alert>
      </v-card>
    </v-dialog>
    </div>
  </v-app>
</template>
  
  
  <script>
  import SideBarAdmin from '../../components/SideBarAdmin.vue';
  import axios from 'axios';
  import AddView from './AddView.vue';
  import EditView from './EditView.vue';
  export default {
  components: { SideBarAdmin, AddView, EditView },
  name:'adminView',
  data(){
          return{
              categories:[],
              dialogAdd: false,
              dialogEdit: false,
              currentItem: '',
              dialogDelete: false,
              categoryId:'',
        }
    },
    methods:{
        getCategories(){
            axios.get('https://652a52484791d884f1fcc90c.mockapi.io/tranquanganh-deso1/quanh')// ('Link api tren swagger')
            .then(response =>{
                this.categories = response.data;
            })
            .catch(error=>{
                console.log(error);
            })
        },
        deleteCategory(){
            axios.delete('https://652a52484791d884f1fcc90c.mockapi.io/tranquanganh-deso1/quanh/' +'/'+ this.categoryId)
            .then(response =>{
                var newArr = this.categories.filter(x => x.categoryId !=this.categoryId);
                this.categories = newArr;
                this.dialogDelete = false;
                console.log(response.status)
            })
            .catch(error=>{
                console.log(error);
            }) 
            
        }
    },
    created(){
        this.getCategories();
    },
    
};
  </script>
  
  <style scoped>
.admin-content {
  padding: 20px;
}

.header-row {
  align-items: center;
  padding: 10px;
  background-color: #2d2d2d;
  border-radius: 8px;
  margin-bottom: 20px;
}

.header-title {
  margin-left: 10px;
  color: #f6d365;
  font-weight: bold;
  align-items: center;
}

.add-btn {
  background-color: #f6d365;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -2px rgba(0, 0, 0, 0.1);
}

.data-card {
  overflow-x: auto;
}

.v-table {
  background-color: #1e1e1e;
  color: white;
  border-radius: 4px;
}

.v-table thead th {
  background-color: #f6d365;
  color: #2d2d2d;
  font-weight: bold;
}

.v-table tbody tr:hover {
  background-color: #424242;
}

.v-btn {
  margin: 0 4px;
}

.v-btn .mdi-icon {
  color: white;
}

/* Responsive adjustments */
@media (max-width: 600px) {
  .header-row, .data-card {
    padding: 5px;
  }

  .header-title, .v-table th, .v-table td {
    font-size: 14px;
  }

  .v-btn {
    min-width: 30px;
    padding: 4px;
  }

  .v-icon {
    font-size: 18px;
  }
}
</style>
  