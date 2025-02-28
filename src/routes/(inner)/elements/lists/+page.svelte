<script lang="ts">
	import DocsShell from '$docs/DocsShell/DocsShell.svelte';
	import { DocsFeature, type DocsShellSettings, type DocsShellTable } from '$docs/DocsShell/types';

	import CodeBlock from '$lib/utilities/CodeBlock/CodeBlock.svelte';

	// Docs Shell
	const settings: DocsShellSettings = {
		feature: DocsFeature.Element,
		name: 'Lists',
		description: 'Provides styles for static list elements.',
		stylesheetIncludes: ['all', 'elements'],
		stylesheets: ['elements/lists'],
		source: 'styles/elements/lists.css'
	};
	const classes: DocsShellTable[] = [
		{
			headings: ['Class', 'Description'],
			source: [
				['<code>.list</code>', 'Class for defining a unordered or ordered list.'],
				['<code>.list-dl</code>', 'Class for defining a description list.'],
				['<code>.list-nav</code>', 'Class for defining a navigation list.']
			]
		}
	];
</script>

<DocsShell {settings} {classes}>
	<!-- Slot: Sandbox -->
	<svelte:fragment slot="sandbox">
		<section class="grid grid-cols-1 md:grid-cols-2 2xl:grid-cols-4 gap-4">
			<div class="card card-body space-y-4">
				<p class="font-bold">Unordered</p>
				<hr />
				<ul class="list">
					{#each ['A', 'B', 'C'] as v}
						<li>
							<span class="badge-icon p-4 bg-primary-500/30">💀</span>
							<span class="flex-auto">
								Item {v}
							</span>
							<span>⋮</span>
						</li>
					{/each}
				</ul>
			</div>
			<div class="card card-body space-y-4">
				<p class="font-bold">Ordered</p>
				<hr />
				<ol class="list">
					{#each ['A', 'B', 'C'] as v, i}
						<li>
							<span class="badge-icon p-4 bg-primary-500/30">{i + 1}</span>
							<span class="flex-auto">
								Item {v}
							</span>
							<span>⋮</span>
						</li>
					{/each}
				</ol>
			</div>
			<div class="card card-body space-y-4">
				<p class="font-bold">Description</p>
				<hr />
				<dl class="list-dl">
					{#each ['A', 'B'] as v}
						<div>
							<span class="badge-icon p-4 bg-primary-500/30">💀</span>
							<span class="flex-auto">
								<dt>Item {v}</dt>
								<dd>Description for {v}</dd>
							</span>
							<span>⋮</span>
						</div>
					{/each}
				</dl>
			</div>
			<div class="card card-body space-y-4">
				<p class="font-bold">Navigation</p>
				<hr />
				<nav class="list-nav">
					<ul>
						{#each ['A', 'B', 'C'] as v}
							<li>
								<a href="/">
									<span class="badge-icon p-4 bg-primary-500/30">💀</span>
									<span class="flex-auto">
										Item {v}
									</span>
									<span>⋮</span>
								</a>
							</li>
						{/each}
					</ul>
				</nav>
			</div>
		</section>
	</svelte:fragment>

	<!-- Slot: Usage -->
	<svelte:fragment slot="usage">
		<div class="space-y-4">
			<p>Create semantic list HTML elements, add the <code>.list</code> class, then ensure you wrap children with <em>span</em> elements allow for flex row layout styling.</p>
		</div>
		<!-- Unordered -->
		<div class="space-y-4">
			<h2>Unordered</h2>
			<CodeBlock
				language="html"
				code={`
<ul class="list">
    <li>
        <span>💀</span>
        <span class="flex-auto">Skeleton</span>
    </li>
	<!-- ... -->
</ul>
            `}
			/>
		</div>
		<!-- Ordered -->
		<div class="space-y-4">
			<h2>Ordered</h2>
			<CodeBlock
				language="html"
				code={`
<ol class="list">
    <li>
        <span>1.</span>
        <span class="flex-auto">Skeleton</span>
    </li>
	<!-- ... -->
</ol>
            `}
			/>
		</div>
		<!-- Description -->
		<div class="space-y-4">
			<h2>Description</h2>
			<p>Note we insert an extra <em>div</em> element to control flex layout and aid with vertical list item spacing.</p>
			<CodeBlock
				language="html"
				code={`
<dl class="list-dl">
    <div>
        <span class="badge bg-primary-500">💀</span>
        <span class="flex-auto">
            <dt>Title</dt>
            <dd>Description</dd>
        </span>
    </div>
	<!-- ... -->
</dl>
            `}
			/>
		</div>
		<!-- Navigation -->
		<div class="space-y-4">
			<h2>Navigation</h2>
			<p>While verbose, we do recommend you use all tags shown below to meet recommended <a href="https://www.w3.org/WAI/tutorials/menus/structure/" target="_blank">accessibility guidelines</a>.</p>
			<CodeBlock
				language="html"
				code={`
<nav class="list-nav">
	<!-- (optionally you can provde a label here) -->
    <ul>
        <li>
            <a href="/">
                <span class="badge bg-primary-500">💀</span>
                <span class="flex-auto">Skeleton</span>
            </a>
        </li>
		<!-- ... -->
    </ul>
</nav>
            `}
			/>
			<p>If you need to highlight an active Navigation List item, we recommend conditionally applying a background color to the anchor tag.</p>
			<CodeBlock language="ts" code={`$: classesActive = (href: string) => (href === $page.url.pathname ? '!bg-primary-500' : '');`} />
			<CodeBlock language="html" code={`<a {href} class="{classesActive(href)}">Page</a>`} />
		</div>
		<!-- Global Styles -->
		<div class="space-y-4">
			<h2>Global Styles</h2>
			<p>Use your global stylesheet to update all instances of this element.</p>
			<CodeBlock
				language="css"
				code={`
.list,
.list-dl,
.list-nav ul {
	@apply space-y-4;
}
            `}
			/>
		</div>
	</svelte:fragment>
</DocsShell>
