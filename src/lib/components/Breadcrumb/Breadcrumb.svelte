<script lang="ts">
	import { setContext } from 'svelte';

	// Props
	export let separator: string = `&rsaquo;`;
	// Props (A11y)
	export let label: string = 'breadcrumb';

	// Context
	setContext('separator', separator);

	// Base Classes
	const cBase: string = 'flex align-center space-x-4';

	// Reactive Classes
	$: classesBase = `${cBase} ${$$props.class ?? ''}`;
</script>

<nav data-testid="breadcrumb" aria-label={label}>
	<ol class="breadcrumb {classesBase}">
		<slot />
	</ol>
</nav>
