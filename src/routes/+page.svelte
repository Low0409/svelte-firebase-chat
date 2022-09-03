<script lang="ts">
	import { initializeApp } from 'firebase/app';
	import { getDatabase, ref, set, push, onValue, onChildAdded } from 'firebase/database';

	const firebaseConfig = {
		apiKey: 'AIzaSyAnxuPoXyfwbGH0OPEDjZEpJyGH2OzjsKw',
		authDomain: 'next-chat-180a7.firebaseapp.com',
		projectId: 'next-chat-180a7',
		storageBucket: 'next-chat-180a7.appspot.com',
		messagingSenderId: '74254041293',
		appId: '1:74254041293:web:a81394eb7ad15c267f6984',
		measurementId: 'G-7T8S9L99M4'
	};

	const app = initializeApp(firebaseConfig);
	const db = getDatabase(app);
	const DB = ref(db, 'chats1/');

	let message_array: any = [];

	onChildAdded(DB, (data) => {
		message_array = [...message_array, data.child('Text').val()];
	});

	const addMessage = () => {
		push(DB, {
			Text: message
		});
	};

	let message = '';
</script>

<svelte:head>
	<title>About</title>
	<meta name="description" content="About this app" />
</svelte:head>

<div class="content">
	<section>
		<picture>
			<source srcset="svelte-welcome.webp" type="image/webp" />
			<img src="svelte-welcome.png" alt="Welcome" />
		</picture>
	</section>
	<ul id="messages_list">
		{#each message_array as m}
			<li>{m}</li>
		{/each}
	</ul>
	<div>
		<input id="text" bind:value={message} />
		<button id="send" on:click={addMessage}>送信</button>
	</div>
</div>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
	}
</style>
