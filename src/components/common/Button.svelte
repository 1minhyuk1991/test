<script lang="ts">
	import { IconTrash, IconPencil, IconCheck, IconXMark } from '../../icons/icons';

	enum ButtonType {
		Save = 'Save',
		Edit = 'Edit',
		Delete = 'Delete',
		Cancel = 'Cancel',
		Default = 'Default',
	}
	const { Save, Edit, Delete, Cancel, Default } = ButtonType;

	export let title: string;
	export let btnType: ButtonType = Default;
	export let isIcon: boolean = false;
	export let size: string = 'sm';
	export let disabled: boolean = false;
	export let onClickF: () => void;

	const icon = () => {
		switch (btnType) {
			case Save:
				return 'bg-blue-600 hover:bg-blue-700 text-white border-blue-600';
			case Edit:
				return 'bg-blue-600 hover:bg-blue-700 text-white border-blue-600';
			case Delete:
				return 'bg-red-600 hover:bg-red-700 text-white border-red-600';
			case Cancel:
				return 'bg-gray-600 hover:bg-gray-700 text-white';
			default:
				return 'bg-white hover:bg-gray-100';
		}
	};

	const isIconStyle: string = isIcon
		? `text-gray-600 hover:text-gray-800`
		: `${icon()} border border-dark-900`;

	const fontSize = (fs: string) => {
		switch (fs) {
			case 'xs':
				return 'text-xs';
			case 'md':
				return 'text-md';
			case 'lg':
				return 'text-lg';
			case 'xl':
				return 'text-xl';

			default:
				return 'text-sm';
		}
	};
</script>

<button
	on:click="{() => {
		if (onClickF) {
			onClickF();
		}
	}}"
	class="{`${fontSize(
		size,
	)} ${isIconStyle} rounded-lg px-4 py-2 font-semibold transition-all disabled:opacity-50`}"
	disabled="{disabled}"
>
	{#if isIcon}
		{#if btnType === Save}
			<IconCheck width="{18}" height="{18}" />
		{:else if btnType === Edit}
			<IconPencil width="{18}" height="{18}" />
		{:else if btnType === Delete}
			<IconTrash width="{18}" height="{18}" />
		{:else if btnType === Cancel}
			<IconXMark width="{18}" height="{18}" />
		{/if}
	{:else}
		{title}
		{#if !title}<slot />{/if}
	{/if}
</button>
