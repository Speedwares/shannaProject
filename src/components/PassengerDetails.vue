<template>
  <div class="home">
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
       <b-form-group id="input-group-23" label="Name:" label-for="input-23">
        <b-form-input
          id="input-23"
          v-model="form.name"
          required
          placeholder="Enter name"
        ></b-form-input>
        </b-form-group>
      <b-form-group id="input-group-24" label="SurName:" label-for="input-24">
        <b-form-input
          id="input-22"
          v-model="form.surname"
          required
          placeholder="Enter Surname"
        ></b-form-input>
      </b-form-group>
      <b-form-group
        id="input-group-1"
        label="Email address:"
        label-for="input-1"
        description="We'll never share your email with anyone else."
      >
        <b-form-input
          id="input-1"
          v-model="form.email"
          type="email"
          required
          placeholder="Enter email"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Food:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="form.food"
          :options="foods"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-4">
        <b-form-checkbox-group v-model="form.checked" id="checkboxes-4">
          <b-form-checkbox value="me">Check me out</b-form-checkbox>
          <b-form-checkbox value="that">Check that out</b-form-checkbox>
        </b-form-checkbox-group>
      </b-form-group>

       <b-form-group id="input-group-34" :label=item.price label-for="input-34"  v-for="item in items" v-bind:key="item.id">
        <b-form-select
          :id=item.id
          :options=item.name
        ></b-form-select>
        <p>{{item.name}}</p>
      </b-form-group>



      <b-button type="submit" variant="primary" v-b-modal.modal-1>Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
<div>

</div>
  </div>
</template>

<script>

import axios from 'axios'

export default {
    data() {
      return {
        form: {
          email: '',
          name: '',
          surname: '',
          food: null,
          checked: []
       
        },
        foods: [{ text: 'Select One', value: null }, 'Carrots', 'Beans', 'Tomatoes', 'Corn'],
        show: true,
        items:[]
      }
    },
    methods: {
      onSubmit(evt) {
        evt.preventDefault()
      
      },
      onReset(evt) {
        evt.preventDefault()
        // Reset our form values
        this.form.email = ''
        this.form.name = ''
        this.form.surname = ''
        this.form.food = null
        this.form.checked = []
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      },
    async fetchItems() {
      const response2 = await axios.get('http://demo4507124.mockable.io/products')
      this.items = response2.data.slice(0, 5)
    }
  },
  created: function(){
    this.fetchItems()
  }
}
  
</script>
