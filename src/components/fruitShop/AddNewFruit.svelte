<script lang="ts">
	import uuid from '../../lib/uuid';
	import { IconArrowPath, IconMinus, IconPlus } from '../../icons/icons';
	import {
		Add,
		Default,
		Delete,
		Fruit,
		Shop,
		basicFruitsData,
		fruits,
		shops,
	} from './fruitShopStore';

	export let shop: Shop | undefined = undefined;

	let selected: Fruit;

	const defaultButtonStyle =
		'flex items-center rounded-full px-2 py-1 text-xs font-semibold text-white transition-all disabled:opacity-30';

	$: alreadyAdded = (id: string) => ($fruits.find((fruit) => fruit.id === id) ? true : false);

	$: buttons = shop
		? [
				{
					id: uuid(),
					keyword: Add,
					title: 'All',
					style: 'text-blue-600 hover:text-blue-800',
					disabled: $fruits.length === 0 || $fruits.length === shop.fruits.length,
					onClick: shops.allAddItems,
				},
				{
					id: uuid(),
					keyword: Delete,
					title: 'All',
					style: 'text-red-600 hover:text-red-800',
					disabled: shop.fruits.length === 0,
					onClick: shops.allDeleteItems,
				},
		  ]
		: [
				{
					id: uuid(),
					keyword: Add,
					title: 'All Add',
					style: 'bg-blue-600 hover:bg-blue-800',
					disabled: basicFruitsData.length === $fruits.length,
					onClick: fruits.allAddItems,
				},
				{
					id: uuid(),
					keyword: Delete,
					title: 'All Delete',
					style: 'bg-red-600 hover:bg-red-800',
					disabled: $fruits.length === 0,
					onClick: fruits.allDeleteItems,
				},
				{
					id: uuid(),
					keyword: Default,
					title: 'Default Fruits',
					style: 'bg-gray-600 hover:bg-gray-800',
					disabled: false,
					onClick: fruits.setDefaultItems,
				},
		  ];
</script>

{#if !shop}
	<label class="py-5"
		>Add New fruit
		<select
			class="mx-2 mt-2"
			bind:value="{selected}"
			on:change="{() => {
				fruits.setItem(selected);
			}}"
		>
			<option selected disabled value="default">Choose option</option>

			{#each basicFruitsData as addFruit (addFruit.id)}
				<option
					value="{addFruit}"
					disabled="{alreadyAdded(String(addFruit.id))}"
					class="disabled:text-gray-300">{addFruit.icon}{addFruit.name}</option
				>
			{/each}
		</select>
	</label>
{/if}

<div class="flex gap-x-2">
	{#each buttons as button (button.id)}
		<button
			class="{defaultButtonStyle} {button.style}"
			disabled="{button.disabled}"
			on:click="{() => {
				button.onClick(shop ? shop.id : '');
			}}"
		>
			{#if button.keyword === Delete}
				<IconMinus width="{16}" height="{16}" />
			{:else if button.keyword === Default}
				<IconArrowPath width="{16}" height="{16}" />
			{:else}
				<IconPlus width="{16}" height="{16}" />
			{/if}
			{button.title}</button
		>
	{/each}
</div>
