<script>
	import { createForm } from 'svelte-forms-lib';

	const { form, handleChange, handleSubmit } = createForm({
		initialValues: {
			type: '',
			title: '',
			description: ''
		},
		onSubmit: (values) => {
			console.log(
				JSON.stringify({
					type: $form.type,
					title: $form.title,
					description: $form.description
				})
			);
			fetch('https://MoccasinYouthfulCells.scidroid.repl.co/add', {
				method: 'POST',
				body: JSON.stringify({
					type: $form.type,
					title: $form.title,
					description: $form.description
				})
			});
		}
	});
</script>

<div class="flex">
	<form on:submit={handleSubmit} class="m-auto w-96 p-6">
		<div class="p-6">
			<label for="title" class="text-gray-700">Tipo</label>
			<select
				class="block w-52 py-2 px-3 border border-gray-300 bg-white rounded-md shadow-sm focus:outline-none focus:ring-primary-500 focus:border-primary-500"
				id="title"
				name="type"
				on:change={handleChange}
				bind:value={$form.type}
			>
				<option />
				<option>Asignacion</option>
				<option>Mensaje</option>
			</select>
		</div>
		{#if $form.type != ''}
			{#if $form.type == 'Asignacion'}
				<div class="p-6">
					<label class="text-gray-700" for="name">Nombre</label>
					<input
						class=" rounded-lg border-transparent flex-1 appearance-none border border-gray-300 w-full py-2 px-4 bg-white text-gray-700 placeholder-gray-400 shadow-sm text-base focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent"
						id="name"
						name="title"
						on:change={handleChange}
						bind:value={$form.title}
					/>
				</div>
			{/if}
			<div class="p-6">
				<label class="text-gray-700" for="email">Mensaje</label>
				<input
					class=" rounded-lg border-transparent flex-1 appearance-none border border-gray-300 w-full py-2 px-4 bg-white text-gray-700 placeholder-gray-400 shadow-sm text-base focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent"
					type="text"
					id="email"
					name="description"
					on:change={handleChange}
					bind:value={$form.description}
				/>
			</div>
			<button
				class="py-2 px-4  bg-indigo-600 hover:bg-indigo-700 focus:ring-indigo-500 focus:ring-offset-indigo-200 text-white w-full transition ease-in duration-200 text-center text-base font-semibold shadow-md focus:outline-none focus:ring-2 focus:ring-offset-2  rounded-lg "
				type="submit">Enviar</button
			>
		{/if}
	</form>
</div>
