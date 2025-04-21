<script lang="ts">
	import type { HTMLTextareaAttributes } from 'svelte/elements';

	type Props = {
		error?: boolean;
		msg?: string;
	};

	let {
		error = false,
		msg = '',
		value = $bindable(),
		...rest
	}: Props & HTMLTextareaAttributes = $props();
</script>

<div class="my-2 flex w-full flex-col">
	<label for={rest.id} class={error ? 'text-red-500' : 'text-black'}>{rest.title || ''}</label>
	<textarea
		{...rest}
		bind:value
		autocomplete="off"
		class={`resize-none rounded-md border px-3 py-2 focus:outline-none disabled:pointer-events-none disabled:bg-gray-200 disabled:opacity-80 disabled:outline-none ${error ? 'border-red-500 text-red-500 placeholder:text-red-500 focus:border-red-500' : 'border-gray-300 focus:border-black'}  ${rest.class || ''}`}
	></textarea>
	{#if error}
		<span class="text-sm text-red-500">{msg}</span>
	{/if}
</div>
