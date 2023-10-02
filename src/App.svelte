<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Poppins:ital@1&display=swap" rel="stylesheet">
<script>
	let users = [
		{
			id: 0,
			name: 'Shruthi',
			age: 26,
			country: 'India'
		},
		{
			id: 1,
			name: 'Kane Williamson',
			age: 31,
			country: 'New Zealand'
		}
	];
	let data = {
		name: '',
		age: '',
		country: '',
		id:null
	};
	let addUser = () => {
		const newUser = {
			id: Date.now() + Math.random(), //To generate a Unique id
			name: data.name,
			age: data.age,
			country: data.country
		};
		// Adding new users to list
		users = users.concat(newUser);
		data = {
			name: '',
			age: '',
			country: '',
			id:null
		};
		console.log(users);
	};

	//For editing the user 
	let isEdit = false;
	let editUser = (user) => {
		isEdit = true;
		data = user;
	};

	let updateUser = () => {
		isEdit = !isEdit;
		let userDB = {
			name: data.name,
			age: data.age,
			country: data.country,
			id: data.id
		};
		let objIndex = users.findIndex((obj) => obj.id == userDB.id);
		users[objIndex] = userDB;
		data = {
			id: null,
			name: '',
			age: '',
			country: ''
		};
	};

	//for deleting the user
	let deleteUser = (id) => {
		console.log(id);
		users = users.filter((user) => user.id !== id);
	};
</script>

<center><h2>CRUD Operations using svelte</h2></center>
<section>
	<h3>Add New User</h3>
	<form>
		<div>
			<label for="name">Name</label>
			<input bind:value={data.name} type="text" id="text" placeholder="Enter Name" />
		</div>
		<div>
			<label for="age">Age</label>
			<input bind:value={data.age} type="number" id="text" placeholder="Enter Age" />
		</div>
		<div>
			<label for="country">Country</label>
			<input bind:value={data.country} type="text" id="text" placeholder="Enter Country" />
		</div>
		{#if isEdit === false}
			<button class="btn" type="submit" on:click|preventDefault={addUser}> Add User </button>
		{:else}
			<button class="btn" type="submit" on:click|preventDefault={updateUser}> Edit User </button>
		{/if}
	</form>
	{#each users as user}
		<div>{user.name} is {user.age} years old and lives in {user.country}

		<button class="btn" on:click={editUser(user)}>Edit</button>
		<button class="btn" on:click={deleteUser(user.id)}>Delete</button>
		</div>
	{/each}
</section>

<style>
	*{
		font-family: 'poppins', 'cursive';
	}
	section{
    	justify-content: center; 
    	align-items: center; 
		width: 585px;
  		border: 4px solid black;
		box-shadow: 5px 10px 5px 10px #888888;
		border-radius: 5%;
  		padding: 50px;
  		margin: 20px;
	}

	.btn{
		background-color: rgb(24, 191, 237) ;
		border-radius: 8px !important;
		color: white;
	}

	.btn:hover{
		background-color: rgb(26, 117, 124);
	}
</style>