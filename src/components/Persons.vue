import VueResource from 'vue-resource'
Import VuePaginator from 'vuejs-paginator'

<template>
	<div class="row">
		<div class="col-md-12">
      {{someData.title}}
			<table border="1">
				<tr v-for="person in listOfPersons">
          <td><a v-bind:href="'#/person/' + person.personId">E</a></td>
					<td>{{person.firstName}}</td>
          <td>{{person.lastName}}</td>
				</tr>
			</table>
		</div>
	</div>
</template>

<script>
  export default {
    data () {
      return {
        listOfPersons: [],
        someData: {title: 'This is a test'}
      }
    },
    created () {
      var resource = this.$resource('/vue-test/persons')
      resource.query({page: 1, per_page: 8}).then((response) => {
        this.listOfPersons = response.data.rows
      }, (response) => {
      // error callback
        console.log('Error:' + response.statusText)
      })
    },
    methods: {
      dummyFunction () {
        console.log('dummy')
      }
    }
  }
</script>
 
 
