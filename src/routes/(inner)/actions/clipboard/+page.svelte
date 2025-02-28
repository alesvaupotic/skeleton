<script lang="ts">
	import DocsShell from '$docs/DocsShell/DocsShell.svelte';
	import { DocsFeature, type DocsShellSettings, type DocsShellTable } from '$docs/DocsShell/types';

	import CodeBlock from '$lib/utilities/CodeBlock/CodeBlock.svelte';
	import { clipboard } from '$lib/actions/Clipboard/clipboard';

	// Docs Shell
	const settings: DocsShellSettings = {
		feature: DocsFeature.Action,
		name: 'Clipboard',
		description: 'Allows you to quickly copy select data to the clipboard.',
		imports: ['clipboard'],
		source: 'actions/Clipboard',
		parameters: true
	};
	const properties: DocsShellTable[] = [
		{
			headings: ['Key', 'Type', 'Description'],
			source: [
				['<code>element</code>', 'string', `HTML element's <em>data-clipboard</em> ID value.`],
				['<code>input</code>', 'string', `Input element's <em>data-clipboard</em> ID value.`]
			]
		}
	];
	const events: DocsShellTable[] = [
		{
			description: 'Coming soon.'
			// headings: ['Selector', 'Description'],
			// source: [
			// 	['<code>.foo</code>', '...'],
			// 	['<code>.bar</code>', '...']
			// ]
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
</script>

<DocsShell {settings} {properties} {events} {classes}>
	<!-- Slot: Sandbox -->
	<svelte:fragment slot="sandbox">
		<section class="card card-body grid grid-cols-1 md:grid-cols-2 gap-4">
			<!-- Element -->
			<div class="space-y-4">
				<div class="bg-surface-50 dark:bg-surface-600 h-20 p-2 px-4 rounded" data-clipboard="exampleElement" contenteditable>
					This <em>div</em> is set to 'contenteditable'. Make changes then tap copy.
				</div>
				<button use:clipboard={{ element: 'exampleElement' }} class="btn btn-ghost">Copy Element Contents</button>
			</div>
			<!-- Input -->
			<div class="space-y-4">
				<textarea class="h-20" data-clipboard="exampleInput">Make changes to this textarea and then tap copy.</textarea>
				<button use:clipboard={{ input: 'exampleInput' }} class="btn btn-ghost">Copy Input Value</button>
			</div>
		</section>
	</svelte:fragment>

	<!-- Slot: Usage -->
	<svelte:fragment slot="usage">
		<div class="space-y-4">
			<p>If your data is available in a basic type (string, integer, etc), you can provide it directly to the action.</p>
			<CodeBlock language="ts" code={`const exampleData: string = 'Your data here.';`} />
			<CodeBlock language="html" code={`<button use:clipboard={exampleData}>Copy</button>`} />
		</div>
		<!-- Element -->
		<div class="space-y-4">
			<h2>HTML Elements</h2>
			<p>
				To copy the <em>innerHTML</em> for an HTML element, we'll need to set a <code>data-clipboard</code> target, then provide the action an object of
				<code>element: 'dataClipboardId'</code>
			</p>
			<CodeBlock
				language="html"
				code={`
<!-- Source -->
<div data-clipboard="exampleElement">(contents)</div>

<!-- Trigger -->
<button use:clipboard={{ element: 'exampleElement' }}>Copy</button>
			`}
			/>
		</div>
		<!-- Inputs -->
		<div class="space-y-4">
			<h2>Form Inputs</h2>
			<p>
				To copy the <em>value</em> of a form input, we'll need to set a <code>data-clipboard</code> target, then provide the action an object of
				<code>input: 'dataClipboardId'</code>
			</p>
			<CodeBlock
				language="html"
				code={`
<!-- Source -->
<input type="text" value="(contents)" data-clipboard="exampleInput"></input>

<!-- Trigger -->
<button use:clipboard={{ input: 'exampleInput' }}>Copy</button>
			`}
			/>
		</div>
	</svelte:fragment>
</DocsShell>
