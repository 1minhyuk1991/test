<script lang="ts">
	import IconFrame from './IconFrame.svelte';
</script>

<!--
@component
@param width - number
@param height - number
@param solid - boolean (solid icon)
@param style - string (using tailwindCSS)
@param strokeWidth - number
-->

<IconFrame props="{$$props}">
	<path stroke-linecap="round" stroke-linejoin="round" d="M4.5 12.75l6 6 9-13.5"></path>
</IconFrame>
