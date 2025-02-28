<script lang="ts">
	import DocsShell from '$docs/DocsShell/DocsShell.svelte';
	import { DocsFeature, type DocsShellSettings, type DocsShellTable } from '$docs/DocsShell/types';

	import CodeBlock from '$lib/utilities/CodeBlock/CodeBlock.svelte';
	import LightSwitch from '$lib/utilities/LightSwitch/LightSwitch.svelte';

	// Docs Shell
	const settings: DocsShellSettings = {
		feature: DocsFeature.Utility,
		name: 'Lightswitch',
		description: `Allows users to toggle between light and dark themes using <a href="https://tailwindcss.com/docs/dark-mode" target="_blank">Tailwind's dark mode</a> feature.`,
		imports: ['LightSwitch'],
		source: 'utilities/LightSwitch'
	};
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
	const a11y: DocsShellTable[] = [
		{ aria: 'https://www.w3.org/WAI/ARIA/apg/patterns/switch/' },
		{
			headings: ['Keys', 'Description'],
			source: [['<kbd>Space</kbd> or <kbd>Enter</kbd>', 'When focus is on the switch, changes the state of the switch.']]
		}
	];
</script>

<DocsShell {settings} {classes} {a11y}>
	<!-- Slot: Sandbox -->
	<svelte:fragment slot="sandbox">
		<section class="card card-body flex justify-center items-center !py-10">
			<LightSwitch />
		</section>
	</svelte:fragment>

	<!-- Slot: Usage -->
	<svelte:fragment slot="usage">
		<section class="space-y-8">
			<section class="space-y-4">
				<p>
					See Tailwind's official <a href="https://tailwindcss.com/docs/dark-mode" target="_blank">dark mode</a> documentation for full instructions. Ensure you've added <code>darkMode: 'class'</code>
					to your <a href="/guides/tailwind">Tailwind config</a>.
				</p>
				<CodeBlock language="html" code={`<LightSwitch />`} />
			</section>
			<div class="space-y-4">
				<h2>How It Works</h2>
				<p>
					By default this will match the <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme" target="_blank">prefers-color-scheme</a> setting in your device's operating
					system settings. However, when toggled, the following will occur.
				</p>
				<ul class="list-disc list-inside space-y-1">
					<li>If dark mode is enabled, a <code>dark</code> class will be applied to your <em>HTML</em> page element.</li>
					<li>All instances of the Light Switch share state and will update accordingly.</li>
					<li>
						A value of <code>mode: 'light | dark'</code> will persist in
						<a href="https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage" target="_blank">window.localStorage</a>.
					</li>
				</ul>
				<CodeBlock language="html" code={`<!-- Light Mode -->\n<html>`} />
				<CodeBlock language="html" code={`<!-- Dark Mode -->\n<html class="dark">`} />
			</div>
			<div class="space-y-4">
				<h2>Utility Stores</h2>
				<p>To check either the user's <em>operating system preferred color</em> scheme or the <em>current lightswitch value</em>, use the following Svelte store values.</p>
				<CodeBlock language="ts" code={`import { storePrefersDarkScheme, storeLightSwitch } from '@brainandbones/skeleton';`} />
				<ul class="list-disc list-inside space-y-1">
					<li><code>storePrefersDarkScheme</code> - The operating system preference. Value will be <em>true</em> for dark, <em>false</em> for light.</li>
					<li><code>storeLightSwitch</code> - <em>true</em> for dark, <em>false</em> for light. If <em>undefined</em>, use the operating system preference.</li>
				</ul>
				<p>Note this may not be accurate if the LightSwitch component has not yet been initialized.</p>
			</div>
		</section>
	</svelte:fragment>
</DocsShell>
