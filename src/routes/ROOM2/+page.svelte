<script lang="ts">
	import Message from '$lib/MessageCompo.svelte';

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
	const DB = ref(db, 'chats/');

	const msg = {
		user: 'dummy_user',
		text: ''
	};

	let message_array: any = [];

	onChildAdded(DB, (data) => {
		message_array = [...message_array, data.child('chat').val()];
		console.log(message_array);
	});

	const addMessage = () => {
		push(DB, {
			chat: msg
		});
	};
</script>

<div class="content">
	<ul id="messages_list">
		{#each message_array as m}
			<Message {...m} />
		{/each}
	</ul>
	<div>
		<input id="text" bind:value={msg.text} />
		<button id="send" on:click={addMessage}>🐸</button>
	</div>
</div>
