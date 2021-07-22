<template>
  <div class="home-view-container"><h1>Adopt a new best friend.</h1>
  <h5>{{ animalsCount }} animals</h5>
  <h5>{{ getAllCats.length }} cats</h5>
    <button @click="togglePetForm" class="btn btn-primary">Add New Pet</button>

     <b-form @submit.prevent="handleSubmit" v-if="showPetForm" class="my-4">
      <b-form-group id="input-group-2" label="Pet's Name:" label-for="input-2" class="my-3">
        <b-form-input
          id="input-2"
          v-model="formData.name"
          placeholder="Enter name"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Species:" label-for="input-3" class="my-3">
        <b-form-select
          id="input-3"
          v-model="formData.species"
          :options="['cats', 'dogs']"
          required
          class="form-control"
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-2" label="Pet's Age:" label-for="input-2" class="my-3">
        <b-form-input
          id="input-2"
          type="number"
          v-model="formData.age"
          placeholder="Enter age"
          required
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary" class="mx-1">Submit</b-button>
      <b-button type="reset" variant="danger" class="mx-1">Reset</b-button>
    </b-form>

  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
export default {
  name: 'Home',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: 0,
        species: null
      }
    }
  },
  computed: {
    ...mapGetters([
      'animalsCount',
      'getAllCats'
    ])
  },
  methods: {
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit () {
      const { species, age, name } = this.formData
      const payload = {
        species,
        pet: {
          name,
          age
        }
      }
      this.addPet(payload)
      // Reset form
      this.formData = {
        name: '',
        age: 0,
        species: null
      }
    },
    ...mapActions([
      'addPet'
    ])
  }
}
</script>
