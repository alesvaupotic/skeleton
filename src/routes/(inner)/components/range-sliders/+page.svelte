<script lang="ts">
	import { writable, type Writable } from 'svelte/store';

	import DocsShell from '$docs/DocsShell/DocsShell.svelte';
	import { DocsFeature, type DocsShellSettings, type DocsShellTable } from '$docs/DocsShell/types';

	import RadioGroup from '$lib/components/Radio/RadioGroup.svelte';
	import RadioItem from '$lib/components/Radio/RadioItem.svelte';
	import RangeSlider from '$lib/components/RangeSlider/RangeSlider.svelte';
	import CodeBlock from '$lib/utilities/CodeBlock/CodeBlock.svelte';

	// Stores
	const storeMax: Writable<number> = writable(50);
	const storeStep: Writable<number> = writable(1);
	const storeTicked: Writable<boolean> = writable(true);

	// Docs Shell
	const settings: DocsShellSettings = {
		feature: DocsFeature.Component,
		name: 'Range Sliders',
		description: 'Capture input from a range of values, including optional ticks.',
		imports: ['RangeSlider'],
		source: 'components/RangeSlider'
	};
	const properties: DocsShellTable[] = [
		{
			headings: ['Prop', 'Type', 'Default', 'Description'],
			source: [
				['<code>value</code>', 'number', '0', 'Set the input value.'],
				['<code>min</code>', 'number', '0', 'Set the input minimum range.'],
				['<code>max</code>', 'number', '100', 'Set the input maximum range.'],
				['<code>step</code>', 'number', '1', 'Set the input step offset.'],
				['<code>ticked</code>', 'boolean', 'false', 'Enables tick marks. See browser support below.'],
				['<code>accent</code>', 'string', 'accent-accent-500', 'Provide classes to set the input accent color.']
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
			headings: ['Prop', 'Description'],
			source: [
				['<code>default</code>', 'A label slot directly above the range slider.'],
				['<code>trail</code>', 'A label slot directly below the range slider.']
			]
		}
	];
	const a11y: DocsShellTable[] = [
		{
			aria: 'https://www.w3.org/WAI/ARIA/apg/patterns/slider/',
			headings: ['Prop', 'Type', 'Description'],
			source: [
				['<code>id</code>', 'string', 'Provide a unique input id.'],
				['<code>label</code>', 'string', `A semantic ARIA label.`]
			]
		},
		{
			label: 'Keyboard Interactions',
			headings: ['Keys', 'Description'],
			source: [
				['<kbd>Right Arrow</kbd> or <kbd>Up Arrow</kbd>', 'Increase the value of the slider by one step.'],
				['<kbd>Left Arrow</kbd> or <kbd>Down Arrow</kbd>', 'Decrease  the value of the slider by one step.'],
				['<kbd>Home</kbd>', 'Set the slider to the first allowed value in its range.'],
				['<kbd>End</kbd>', 'Set the slider to the last allowed value in its range.'],
				['<kbd>Page Up</kbd>', 'Increase the slider value by an amount larger than the step change made by <kbd>Up Arrow</kbd>.'],
				['<kbd>Page Down</kbd>', 'Decrease  the slider value by an amount larger than the step change made by <kbd>Up Down</kbd>.']
			]
		}
	];

	// Reactive Props
	$: props = {
		label: 'Skeleton',
		value: $storeMax / 2,
		min: 0,
		max: $storeMax,
		step: $storeStep,
		ticked: $storeTicked,
		accent: 'accent-accent-500'
	};
</script>

<DocsShell {settings} {properties} {classes} {slots} {a11y}>
	<!-- Slot: Sandbox -->
	<svelte:fragment slot="sandbox">
		<section class="space-y-4 xl:space-y-0 xl:grid grid-cols-[1fr_auto] gap-2">
			<!-- Example -->
			<div class="card card-body flex justify-center items-center">
				<!-- prettier-ignore -->
				<svelte:component
						this={RangeSlider}
						label={props.label}
						bind:value={props.value}
						max={props.max}
						step={props.step}
						ticked={props.ticked}
						accent={props.accent}
						class="w-full lg:max-w-[75%] max-auto"
					>
						<div class="flex justify-between items-center">
							<div>{props.label}</div>
							<div class="text-xs">{props.max}</div>
						</div>
						<svelte:fragment slot="trail">
							<p class="text-center">Value <code>{props.value}</code></p>
						</svelte:fragment>
					</svelte:component>
			</div>
			<!-- Options -->
			<div class="card card-body space-y-4">
				<!-- Label -->
				<label>
					<span>Label</span>
					<input type="text" bind:value={props.label} placeholder="Label" />
				</label>
				<!-- Max -->
				<label for="">
					<span>Max</span>
					<RadioGroup selected={storeMax} display="flex">
						<RadioItem value={10}>10</RadioItem>
						<RadioItem value={50}>50</RadioItem>
						<RadioItem value={100}>100</RadioItem>
					</RadioGroup>
				</label>
				<!-- Step -->
				<label for="">
					<span>Step</span>
					<RadioGroup selected={storeStep} display="flex">
						<RadioItem value={1}>1</RadioItem>
						<RadioItem value={5}>5</RadioItem>
						<RadioItem value={10}>10</RadioItem>
					</RadioGroup>
				</label>
				<div class="grid grid-cols-2 gap-4">
					<!-- Ticks -->
					<label for="">
						<span>Ticks</span>
						<RadioGroup selected={storeTicked} display="flex">
							<RadioItem value={false}>Off</RadioItem>
							<RadioItem value={true}>On</RadioItem>
						</RadioGroup>
					</label>
					<!-- Accent -->
					<label>
						<span>Accent</span>
						<select name="accent" id="accent" bind:value={props.accent}>
							<option value="accent-primary-500">accent-primary-500</option>
							<option value="accent-accent-500">accent-accent-500</option>
							<option value="accent-ternary-500">accent-ternary-500</option>
							<option value="accent-warning-500">accent-warning-500</option>
							<option value="accent-surface-500">accent-surface-500</option>
						</select>
					</label>
				</div>
			</div>
		</section>
	</svelte:fragment>

	<!-- Slot: Usage -->
	<svelte:fragment slot="usage">
		<CodeBlock language="html" code={`<RangeSlider bind:value={50} max={100} step={5} ticked>Label</RangeSlider>`} />
	</svelte:fragment>
</DocsShell>
