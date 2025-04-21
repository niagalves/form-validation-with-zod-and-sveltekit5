<script lang="ts">
	import type { HTMLButtonAttributes } from 'svelte/elements';

	let {
		children,
		...rest
	}: {
		children: any;
	} & HTMLButtonAttributes = $props();
</script>

<button
	{...rest}
	class={`w-full cursor-pointer rounded-md bg-black px-4 py-2 text-base font-semibold
  text-white
  transition ease-in hover:bg-black/85 disabled:pointer-events-none disabled:bg-gray-200
  disabled:text-gray-400 disabled:opacity-80 disabled:outline-none
  ${rest.class || ''}`}>{@render children?.()}</button
>
