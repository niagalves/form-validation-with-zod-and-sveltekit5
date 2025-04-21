<script>
	import Button from '$lib/components/Button.svelte';
	import Checkbox from '$lib/components/Checkbox.svelte';
	import Input from '$lib/components/Input.svelte';
	import Textarea from '$lib/components/Textarea.svelte';
</script>

<main class="min-h-screen w-full p-4">
	<div class="mx-auto max-w-4xl">
		<h1 class="text-2xl font-black">Form</h1>
		<form action="">
			<Input type="text" title="Name" id="name" placeholder="full name" />
			<Input type="email" title="E-mail" placeholder="e-mail" id="email" />
			<Textarea title="description" placeholder="Description" id="Description" />
			<p class="text-lg font-bold">How would you like to receive information?*</p>
			<Checkbox type="checkbox" title="E-mail" id="test" />
			<Checkbox type="checkbox" title="Telegram" id="test" />
			<Checkbox type="checkbox" title="WhatsApp" id="test" />
			<p class="text-lg font-bold">You like animals*</p>
			<div class="flex w-2xs flex-col items-center">
				<Input type="radio" title="Yes" placeholder="Yes" id="likeAnimals" />
				<Input type="radio" title="No" placeholder="No" id="likeAnimals" />
			</div>
			<div class="my-2">
				<Button type="button">Submit</Button>
			</div>
		</form>
	</div>
</main>
