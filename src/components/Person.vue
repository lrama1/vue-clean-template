import VueResource from 'vue-resource'

<template>
	<div class="row">
		<div class="form-group">
			<label for="firstName">First Name</label>
			<input class="form-control" id="firstName" placeholder="First Name" v-model="person.firstName">
		</div>
		<div class="form-group">
			<label for="lastName">Last Name</label>
			<input class="form-control" id="lastName" placeholder="Last Name" v-model="person.lastName">
		</div>
		<div>
			<button type="button" class="btn btn-primary" @click="savePerson">Save</button>
			<button type="button" class="btn btn-primary" @click="updatePerson">Update</button>
		</div>
	</div>
</template>

<script>
  export default {
    data () {
      let person = {
        firstName: '',
        lastName: ''
      }
      return {
        person
      }
    },
    created () {
      console.log(this.$route.params.id)
      if (this.$route.params.id) {
        console.log('found a value')
        var resource = this.$resource('/vue-test/person/' + this.$route.params.id)
        resource.query().then((response) => {
          this.person = response.data
        }, (response) => {
        // error callback
          console.log('Error:' + response.statusText)
        })
      }
    },
    methods: {
      savePerson () {
        console.log(this.person)
        var resource = this.$resource('/vue-test/person')
        resource.save(this.person).then((response) => {
        // success callback
        }, (response) => {
        // error callback
          console.log('Error:' + response.statusText)
        })
      },
      updatePerson () {
        console.log(this.person)
        var resource = this.$resource('/vue-test/person')
        resource.update(this.person).then((response) => {
        // success callback
        }, (response) => {
        // error callback
        })
      }
    }
  }
</script>
