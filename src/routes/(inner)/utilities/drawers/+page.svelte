<script lang="ts">
	import { writable, type Writable } from 'svelte/store';

	import DocsShell from '$docs/DocsShell/DocsShell.svelte';
	import { DocsFeature, type DocsShellSettings, type DocsShellTable } from '$docs/DocsShell/types';

	import Drawer from '$lib/utilities/Drawer/Drawer.svelte';
	import CodeBlock from '$lib/utilities/CodeBlock/CodeBlock.svelte';

	// Stores
	const storeDrawer: Writable<boolean> = writable(false);

	// Docs Shell
	const settings: DocsShellSettings = {
		feature: DocsFeature.Utility,
		name: 'Drawers',
		description: 'Displays an overlay panel that attaches to any side of the screen.',
		imports: ['Drawer'],
		source: 'utilities/Drawer'
	};
	const properties: DocsShellTable[] = [
		{
			headings: ['Prop', 'Type', 'Default', 'Values', 'Required', 'Description'],
			source: [
				['<code>open</code>', 'writable(boolean)', 'writable(false)', 'boolean', '&check;', 'Provide a store to manage visible state.'],
				['<code>position</code>', 'string', 'left', 'left | right | top | bottom', '-', 'Set the anchor position.'],
				['<code>duration</code>', 'number', '150', 'milliseconds', '-', 'Define the Svelte transition animation duration.']
			]
		},
		{
			label: 'Drawer',
			description: 'Apply these props to the Drawer component.',
			headings: ['Prop', 'Type', 'Default', 'Description'],
			source: [
				['<code>bgDrawer</code>', 'string', 'bg-surface-100 dark:bg-surface-800', 'Provide classes to set the drawer background color.'],
				['<code>border</code>', 'string', '-', 'Provide classes to set border color.'],
				['<code>rounded</code>', 'string', '-', 'Provide classes to set border radius.'],
				['<code>width</code>', 'string', '(based on position)', 'Provide classes to override the width.'],
				['<code>height</code>', 'string', '(based on position)', 'Provide classes to override the height.'],
				['<code>margin</code>', 'string', '-', 'Provide classes to set margins.']
			]
		},
		{
			label: 'Backdrop',
			description: 'Apply these props to the Drawer component.',
			headings: ['Prop', 'Type', 'Default', 'Description'],
			source: [
				['<code>bgBackdrop</code>', 'string', 'bg-surface-400/70 dark:bg-surface-900/70', 'Provide classes to set the backdrop background color'],
				['<code>blur</code>', 'string', 'backdrop-blur-sm', 'Provide classes to set the blur style.']
			]
		}
	];
	const classes: DocsShellTable[] = [
		{
			description: 'Coming soon.'
			// headings: ['Selector', 'Description'],
			// source: [
			// 	['<code>.foo</code>', '...'],
			// 	['<code>.bar</code>', '...']
			// ]
		}
	];
	const slots: DocsShellTable[] = [
		{
			headings: ['Name', 'Description'],
			source: [['<code>default</code>', 'Provide your Drawer content here.']]
		}
	];
	const a11y: DocsShellTable[] = [
		{ aria: 'https://www.w3.org/WAI/ARIA/apg/patterns/dialogmodal/' },
		{
			headings: ['Prop', 'Type', 'Description'],
			source: [
				['<code>labelledby</code>', 'string', 'Provide an ID of the element labeling the drawer.'],
				['<code>describedby</code>', 'string', 'Provide an ID of the element describing the drawer.']
			]
		},
		{
			label: 'Keyboard Interactions',
			headings: ['Keys', 'Description'],
			source: [['<kbd>Esc</kbd>', ' Closes the drawer.']]
		}
	];

	// Local
	let position: string = 'left';

	// prettier-ignore
	function trigger(p: string): void {
		position = p;
		setTimeout(() => { storeDrawer.set(true); }, 100);
	}
</script>

<Drawer open={storeDrawer} {position}>
	<div class="w-full h-full flex justify-center items-center">
		<div class="text-center">
			<h4>Drawer: <span class="capitalize">{position}</span></h4>
			<p>Tap outside the drawer to close.</p>
		</div>
	</div>
</Drawer>

<DocsShell {settings} {properties} {classes} {slots} {a11y}>
	<!-- Slot: Sandbox -->
	<svelte:fragment slot="sandbox">
		<div class="card card-body text-center space-y-4">
			<p>Select a drawer position to preview.</p>
			<!-- prettier-ignore -->
			<div class="flex justify-center items-center space-x-4">
				<button class="btn-icon btn-ghost" on:click={() => { trigger('left'); }}>&larr;</button>
				<button class="btn-icon btn-ghost" on:click={() => { trigger('right'); }}>&rarr;</button>
				<button class="btn-icon btn-ghost" on:click={() => { trigger('top'); }}>&uarr;</button>
				<button class="btn-icon btn-ghost" on:click={() => { trigger('bottom'); }}>&darr;</button>
			</div>
		</div>
	</svelte:fragment>

	<!-- Slot: Usage -->
	<svelte:fragment slot="usage">
		<section class="space-y-4">
			<h2>Create a Store</h2>
			<p>Create a <a href="https://svelte.dev/tutorial/writable-stores" target="_blank">Svelte writable store</a> to manage the state of the drawer.</p>
			<CodeBlock language="typescript" code={`import { writable, type Writable } from 'svelte/store';`} />
			<CodeBlock language="typescript" code={`const storeDrawer: Writable<boolean> = writable(false);`} />
		</section>
		<section class="space-y-4">
			<h2>Implement Drawer</h2>
			<p>Pass the store to the Drawer component. For best results implement your Drawer component in your applications root scope.</p>
			<CodeBlock
				language="html"
				code={`
<Drawer open={storeDrawer} position="left">
	(contents)
</Drawer>
        `}
			/>
		</section>
		<section class="space-y-4">
			<h2>Open and Close Triggers</h2>
			<p>Set the store value to <em>true</em> too open the drawer.</p>
			<CodeBlock language="typescript" code={`const drawerOpen: any = () => { storeDrawer.set(true) };`} />
			<CodeBlock language="html" code={`<button on:click={drawerOpen}>Open</button>`} />
			<p>Set the store value to <em>false</em> too close the drawer. You can also tap the backdrop or hit <kbd>ESC</kbd> on your keyboard.</p>
			<CodeBlock language="typescript" code={`const drawerClose: any = () => { storeDrawer.set(false) };`} />
			<CodeBlock language="html" code={`<button on:click={drawerClose}>Close</button>`} />
		</section>
		<section class="space-y-4">
			<h2>Pairing with App Shell</h2>
			<p>Place the Drawer above and outside the App Shell in your root layout. This will prevent page content shifting as the Drawer changes state.</p>
			<CodeBlock language="html" code={`<Drawer></Drawer>\n\n<AppShell></AppShell>`} />
		</section>
	</svelte:fragment>
</DocsShell>
