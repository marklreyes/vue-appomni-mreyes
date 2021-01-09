<template>
	<div id="rolodex">
		<form>
			<input type="text" v-model="name" placeholder="Name">
			<input type="text" v-model="email" placeholder="Email">
			<input type="text" v-model="phone" placeholder="Phone">
			<button @click="addContact">Add</button>
		</form>
		<hr>
		<table>
			<thead>
				<tr>
					<td>Name</td>
					<td>Email</td>
					<td>Phone</td>
					<td>&nbsp;</td>
				</tr>
			</thead>
			<tbody>
				<!-- v-for -->
				<tr v-bind:key="contact.id" v-for="contact in totalContacts">
					<td>{{contact.name}}</td>
					<td>{{contact.email}}</td>
					<td>{{contact.phone}}</td>
					<td><button @click="deleteContact(contact.id)">Delete Contact</button></td>
				</tr>
			</tbody>
		</table>
	</div>
</template>

<script>
export default {
  name: 'RolodexForm',
  data() {
	return {
		name: '',
		email: '',
		phone: '',
		totalContacts: [{
			id: 12345,
			name: 'Isaac',
			email: 'isaac@isaac.com',
			phone: '911'
		}, {
			id: 67890,
			name: 'John',
			email: 'john@john.com',
			phone: '411'
		}]
	}
  },
  methods: {
	addContact(e) {
		e.preventDefault();
		const contact = {
			id: Math.random().toString(32),
			name: this.name,
			email: this.email,
			phone: this.phone
		}
		this.totalContacts.push(contact);
		// clear form fields
		this.name = '';
		this.email = '';
		this.phone = '';
	},
	deleteContact(id) {
		// arr.findIndex(callback( element[, index[, array]] )[, thisArg])
		const index = this.totalContacts.findIndex( (contact) => id === contact.id );
		console.log('delete this index', index); // 0, 1
		this.totalContacts.splice(index, 1);
	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
