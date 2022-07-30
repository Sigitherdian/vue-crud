<template>
<div class="customer-table">
  <table class="table table-bordered">
  <thead class="thead-dark">
    <tr> 
      <th scope="col">Nama</th>
      <th scope="col">Jabatan</th>  
      <th scope="col">Gender</th>
      <th scope="col">Tindakan</th>
    </tr>
  </thead>
  <tbody> 
    <tr v-for="customer in customers" :key="customer.id">
    <template v-if="customerId === customer.id">
      <td>
        <label for="name" class="font-weight-bold">Name :</label>
        <div> 
          <input type="text" v-model="customer.name" class="form-control" />
        </div>
      </td>
      <td>
        <label for="email" class="font-weight-bold">Jabatan:</label>
        <div> 
          <input type="text" v-model="customer.jabatan" class="form-control" />
        </div>
      </td>
      <td>
        <label for="address" class="font-weight-bold">Gender:</label>
        <div> 
          <input type="text" v-model="customer.gender" class="form-control"  />
        </div>
      </td>
      <td> 
        <div class="mt-4">
        <button class="btn btn-success m-2" @click="saveEdit(customer)">Save</button>
        <button class="btn btn-danger" @click="cancelEdit(customer)" >Cancel</button>
        </div>
      </td>
    </template>
    <template v-else>
      <td>{{customer.name}}</td>
      <td>{{customer.jabatan}}</td>
      <td>{{customer.gender}}</td>
      <td>
        <div class="text-center">
         <button class="btn btn-primary mr-2" @click="editCustomer(customer)">Edit</button>
         <button class="btn btn-danger" @click="deleteCustomer(customer.id)">Hapus</button> 
        </div>
      </td>
    </template>
  </tr>
  </tbody>
</table>
</div>
</template>

<script>
  export default {
    name: 'customer-table', 
    props: {
      customers: Array,
    },
    data() {
      return {
          customerId: null,
        }
    },
      //edit customer
      methods: {
        editCustomer(customer) { 
          this.data = Object.assign({}, customer)
          this.customerId = customer.id 
        },
        //Edit-save customer
        saveEdit(customer) { 
          let id = this.data.id
          this.$emit('edit-customer', id, customer)  
          this.customerId = null
        },
        //cancel-edit customer
        cancelEdit(customer) { 
          Object.assign(customer, this.data)
          this.customerId = null;
        },
        //delete customer
        deleteCustomer(id){
          this.$emit('delete-customer', id)  
        }
      }
  }
</script>

<style scoped> 
</style> 