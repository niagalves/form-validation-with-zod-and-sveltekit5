<script lang="ts">
	import { z } from 'zod';
	import Button from '$lib/components/Button.svelte';
	import Checkbox from '$lib/components/Checkbox.svelte';
	import Input from '$lib/components/Input.svelte';
	import Textarea from '$lib/components/Textarea.svelte';

	export const formSchema = z.object({
		name: z.string().min(1, 'Min 1').max(120, 'Max 120'),
		email: z.string().min(1, 'Min 1').max(120, 'Max 120').email('Invalid e-mail'),
		description: z.string().min(6, 'Min. 6').max(300, 'Max. 300'),
		receiveInfo: z
			.array(z.enum(['email', 'telegram', 'whatsapp']))
			.min(1, 'Select at least one method of receiving information'),
		likeAnimals: z.enum(['yes', 'no'], {
			errorMap: () => ({ message: 'Please select if you like animals' })
		})
	});

	let form = $state({
		name: '',
		email: '',
		description: '',
		receiveEmail: false,
		receiveTelegram: false,
		receiveWhatsapp: false,
		likeAnimals: ''
	});

	let errors = $state<any>();

	async function handleSubmit(event: SubmitEvent) {
		event.preventDefault();

		const formData = {
			name: form.name,
			email: form.email,
			description: form.description,
			receiveInfo: [
				form.receiveEmail && 'email',
				form.receiveTelegram && 'telegram',
				form.receiveWhatsapp && 'whatsapp'
			].filter(Boolean),
			likeAnimals: form.likeAnimals
		};

		const result = formSchema.safeParse(formData);

		if (!result.success) {
			const fieldErrors = result.error.flatten().fieldErrors;
			errors = fieldErrors;
		}
	}
</script>

<main class="min-h-screen w-full p-4">
	<div class="mx-auto max-w-4xl">
		<h1 class="text-2xl font-black">Form</h1>
		<form onsubmit={handleSubmit} novalidate>
			<Input
				type="text"
				title="Name"
				id="name"
				placeholder="full name"
				bind:value={form.name}
				required
				error={Boolean(errors?.name?.[0])}
				msg={errors?.name?.[0]}
				minlength={1}
				maxlength={120}
			/>
			<Input
				type="email"
				title="E-mail"
				placeholder="e-mail"
				id="email"
				bind:value={form.email}
				required
				error={Boolean(errors?.email?.[0])}
				msg={errors?.email?.[0]}
				minlength={1}
				maxlength={120}
			/>
			<Textarea
				title="description"
				placeholder="Description"
				id="Description"
				bind:value={form.description}
				required
				error={Boolean(errors?.description?.[0])}
				msg={errors?.description?.[0]}
				minlength={6}
				maxlength={300}
			/>
			<p class="text-lg font-bold">How would you like to receive information?*</p>

			<Checkbox
				type="checkbox"
				title="E-mail"
				value="email"
				bind:checked={form.receiveEmail}
				error={Boolean(errors?.receiveInfo?.[0])}
				msg={errors?.receiveInfo?.[0]}
			/>
			<Checkbox
				type="checkbox"
				title="Telegram"
				value="telegram"
				bind:checked={form.receiveTelegram}
				error={Boolean(errors?.receiveInfo?.[0])}
				msg={errors?.receiveInfo?.[0]}
			/>
			<Checkbox
				type="checkbox"
				title="WhatsApp"
				value="whatsapp"
				bind:checked={form.receiveWhatsapp}
				error={Boolean(errors?.receiveInfo?.[0])}
				msg={errors?.receiveInfo?.[0]}
			/>

			<p class="text-lg font-bold">You like animals?*</p>
			<div class="flex w-2xs flex-col items-center">
				<Input
					type="radio"
					title="Yes"
					placeholder="Yes"
					onclick={() => {
						form.likeAnimals = 'yes';
					}}
					checked={form.likeAnimals === 'yes'}
					error={Boolean(errors?.likeAnimals?.[0])}
					msg={errors?.likeAnimals?.[0]}
					required
				/>
				<Input
					type="radio"
					title="No"
					placeholder="No"
					id="likeAnimals"
					onclick={() => {
						form.likeAnimals = 'no';
					}}
					checked={form.likeAnimals === 'no'}
					error={Boolean(errors?.likeAnimals?.[0])}
					msg={errors?.likeAnimals?.[0]}
					required
				/>
			</div>
			<div class="my-2">
				<Button type="submit">Submit</Button>
			</div>
		</form>
	</div>
</main>
