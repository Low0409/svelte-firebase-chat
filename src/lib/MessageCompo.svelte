<script lang="ts">
	export let user: string;
	export let text: string;
</script>

<div>
	<div class="flex">
		<p>{text}</p>
		<p class="u_id">@{user}</p>
	</div>
</div>

<style>
	.flex {
		display: flex;
	}
	.u_id {
		color: rgb(72, 201, 201);
	}
</style>
