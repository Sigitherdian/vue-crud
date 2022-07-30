<template>
  <div class="customer-form">
    <form @submit.prevent="submit">
      <div class="form-group">
        <label for="name">Nama</label>
        <input type="text" v-model="customer.name" class="form-control" placeholder="Masukan nama pelanggan">
      </div>
      <div class="form-group">
        <label for="email">Jabatan</label>
        <input type="text" v-model="customer.jabatan" class="form-control" placeholder="Masukan email pelanggan">
      </div>
      <div class="form-group">
        <label for="address">Gender</label>
        <textarea type="text" v-model="customer.gender" class="form-control" 
          placeholder="Masukan alamat pelanggan"> </textarea>
      </div>
      <button type="submit" class="btn btn-primary mr-2">Submit</button>
      <button class="btn btn-danger" type="button" data-toggle="collapse" data-target="#collapseExample">
        Cancel
        </button>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'customer-form', 
    data(){
      return {
        customer: {
          name: '',
          jabatan: '',
          gender: '',
        }
      }
    },
  //add new costumer
    methods: {
        submit() {
          this.$emit('add-customer', this.customer)
          this.customer = {
          name: '',
          jabatan: '',
          gender: '',
        }
      },
    },
  }
</script>