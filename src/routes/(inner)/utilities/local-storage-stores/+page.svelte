<script lang="ts">
	import DocsShell from '$docs/DocsShell/DocsShell.svelte';
	import { DocsFeature, type DocsShellSettings } from '$docs/DocsShell/types';

	import CodeBlock from '$lib/utilities/CodeBlock/CodeBlock.svelte';

	// Docs Shell
	const settings: DocsShellSettings = {
		feature: DocsFeature.Utility,
		name: 'Local Storage Store',
		description: 'An extended version of the <a href="https://svelte.dev/tutorial/writable-stores" target="_blank">Svelte writable store</a> that includes pub/sub to local storage.',
		imports: ['localStorageStore'],
		source: 'utilities/LocalStorageStore'
	};
</script>

<DocsShell {settings}>
	<!-- Slot: Usage -->
	<svelte:fragment slot="usage">
		<section class="space-y-4">
			<p>The first parameter <code>storeExample</code> is the local storage key name. The second parameter is the initial value of the store.</p>
			<CodeBlock language="ts" code={`import type { Writable } from 'svelte/store';`} />
			<CodeBlock language="ts" code={`const storeExample: Writable<string> = localStorageStore('storeExample', 'initialValueHere');`} />
			<p>
				This operates exactly like a standard Svelte writable store but with the added benefit of automatic persistence via <a
					href="https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage"
					target="_blank">Local Storage</a
				>.
			</p>
			<CodeBlock
				language="ts"
				code={`
import { get } from 'svelte/store';

// Subscribe to the store
storeExample.subscribe(() => {});

// Update the value
storeExample.update(() => {});

// Set the value
storeExample.set(() => {});

// Read the value
get(storeExample);

// Read value with automatic subscription
$storeExample
        `}
			/>
		</section>
		<!-- Attribution -->
		<section class="space-y-4">
			<h2>Attribution</h2>
			<p>
				<a href="https://github.com/joshnuss/svelte-local-storage-store" target="_blank">Source code</a> provided courtesy of <a href="https://github.com/joshnuss" target="_blank">Joshua Nussbaum</a>.
				Please consider
				<a href="https://github.com/sponsors/joshnuss" target="_blank">sponsoring his work</a>.
			</p>
		</section>
	</svelte:fragment>
</DocsShell>
