<script lang="ts">
	import DocsShell from '$docs/DocsShell/DocsShell.svelte';
	import { DocsFeature, type DocsShellSettings, type DocsShellTable } from '$docs/DocsShell/types';

	import SlideToggle from '$lib/components/SlideToggle/SlideToggle.svelte';
	import CodeBlock from '$lib/utilities/CodeBlock/CodeBlock.svelte';

	// Docs Shell
	const settings: DocsShellSettings = {
		feature: DocsFeature.Component,
		name: 'Slide Toggles',
		description: 'A sliding toggle element that can capture input from a user.',
		imports: ['SlideToggle'],
		source: 'components/SlideToggle'
	};
	const properties: DocsShellTable[] = [
		{
			headings: ['Prop', 'Type', 'Default', 'Values', 'Description'],
			source: [
				['<code>checked</code>', 'boolean', 'false', 'true | false', 'The checked state of the input element.'],
				['<code>accent</code>', 'string', 'bg-accent-500', 'class', 'Provide classes to set the checked state color.'],
				['<code>size</code>', 'string', 'md', 'sm | md | lg', 'Sets the size of the component.']
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
			source: [['<code>default</code>', 'Provide label text.']]
		}
	];
	const a11y: DocsShellTable[] = [
		{
			aria: 'https://www.w3.org/WAI/ARIA/apg/',
			headings: ['Prop', 'Required', 'Description'],
			source: [['<code>label</code>', '-', `Provide a semantic label.`]]
		}
	];

	// Local
	let checkedValue: boolean = false;
</script>

<DocsShell {settings} {properties} {classes} {slots} {a11y}>
	<!-- Slot: Sandbox -->
	<svelte:fragment slot="sandbox">
		<section class="grid grid-cols-1 lg:grid-cols-3 gap-4">
			<div class="card card-body flex justify-center items-center space-x-4">
				<SlideToggle size="sm" accent="bg-primary-500" checked label="Toggle Primary" />
				<SlideToggle size="md" checked label="Toggle Purple" />
				<SlideToggle size="lg" accent="bg-ternary-500" checked label="Toggle Ternary" />
			</div>
			<div class="card card-body flex justify-center items-center space-x-4">
				<SlideToggle size="md" bind:checked={checkedValue}>
					<code class="inline-block w-[40px] text-center">{checkedValue ? 'On' : 'Off'}</code>
				</SlideToggle>
			</div>
			<div class="card card-body flex justify-center items-center space-x-4">
				<SlideToggle disabled label="Toggle Disabled">Disabled</SlideToggle>
			</div>
		</section>
	</svelte:fragment>

	<!-- Slot: Usage -->
	<svelte:fragment slot="usage">
		<section class="space-y-4">
			<CodeBlock language="typescript" code={`let valueChecked: boolean = false;`} />
			<CodeBlock language="html" code={`<SlideToggle bind:checked={valueChecked}>(label)</SlideToggle>`} />
		</section>
		<section class="space-y-2">
			<h2>Size</h2>
			<p>Set <code>size</code> to <em>sm</em>, <em>md</em>, or <em>lg</em>.</p>
			<CodeBlock language="html" code={`<SlideToggle bind:checked={valueChecked} size="lg" />`} />
		</section>
		<section class="space-y-2">
			<h2>Disabled</h2>
			<CodeBlock language="html" code={`<SlideToggle bind:checked={valueChecked} disabled />`} />
		</section>
	</svelte:fragment>
</DocsShell>
