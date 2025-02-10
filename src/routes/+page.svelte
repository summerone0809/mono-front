<script>
    // 1-1.Introduction
    //import Nested from './Nested.svelte';
    let name = 'Svelte';
    let src = '/cool-fun.gif';
    let alt = 'A cat';
    let string = `this string contains some <strong>HTML!!!</strong>`;
    let count = 0;
    $: doubled = count * 2;
    $: {
        console.log(`the count is ${count}`);
        console.log(`this will also be logged whenever count changes`);
        if (count >= 10) {
            alert('count is dangerously high!');
            count = 0;
        }
    }

    // 1-2.Reaactivity
    function  increment(){
        count += 1;
    }

    let numbers = [1, 2, 3, 4];

	function addNumber() {
		numbers = [...numbers, numbers.length + 1];
	}

	$: sum = numbers.reduce((total, currentNumber) => total + currentNumber, 0);

    // 1-3.Props
    import Nested from './Nested.svelte';
    // @ts-ignore
    import PackageInfo from './PackageInfo.svelte';


    const pkg = {
		name: 'svelte',
		speed: 'blazing',
		version: 4,
		website: 'https://svelte.dev'
	};
    //1-4.Logic
    let countA = 0;

	function incrementA() {
		countA += 1;
	}

    const colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet'];
	let selectedA = colors[0];
    import Thing from './Thing.svelte';

    let things = [
        { id: 1, name: 'apple' },
        { id: 2, name: 'banana' },
        { id: 3, name: 'carrot' },
        { id: 4, name: 'doughnut' },
        { id: 5, name: 'egg' }
    ];

    function handleClick() {
        things = things.slice(1);
    }

    import { getRandomNumber } from './utils.js';

    let promise = getRandomNumber();

    function handleClickA() {
        promise = getRandomNumber();
    }

    //1-5.Events
    let m = { x: 0, y: 0 };

	function handleMove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}
    //import Inner from './Inner.svelte';
    import Outer from './Outer.svelte';

	function handleMessage(event) {
		alert(event.detail.text);
	}

    import BigRedButton from './BigRedButton.svelte';
	import horn from '../lib/horn.mp3';

    // const audio = new Audio();
	// audio.src = horn;

	function handleClickB() {
		// audio.load();
		// audio.play();
	}

    //1-6.Binding
    let nameA = 'world';

    let a = 1;
	let b = 2;

    let yes = false;

    let questions = [
		{
			id: 1,
			text: `Where did you go to school?`
		},
		{
			id: 2,
			text: `What is your mother's name?`
		},
		{
			id: 3,
			text: `What is another personal fact that an attacker could easily find with Google?`
		}
	];

	let selected;

	let answer = '';

	function handleSubmit() {
		alert(
			`answered question ${selected.id} (${selected.text}) with "${answer}"`
		);
	}

    let scoops = 1;
	let flavours = [];

	const formatter = new Intl.ListFormat('en', { style: 'long', type: 'conjunction' });

    import { marked } from 'marked';
  
	let value = `Some words are *italic*, some are **bold**\n\n- lists\n- are\n- cool`;
</script>


<!-- 1-1.Introduction -->
<h1>Welcome to {name.toUpperCase()}</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>
<img {src} alt="{alt} dance"/>
<!--<Nested/>-->
<p>{@html string}</p>
<!-- 1-2.Reaactivity -->
<button on:click={increment}>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button> 
<p>{count} doubled is {doubled}</p>

<p>{numbers.join(' + ')} = {sum}</p>

<button on:click={addNumber}>
	Add a number
</button>

<!-- 1-3.Props -->
<Nested answer={'42'} />
<Nested />
<PackageInfo {...pkg} />

<!-- 1-4.Logic -->
<button on:click={incrementA}>
	Clicked {countA}
	{countA === 1 ? 'time' : 'times'}
</button>
{#if countA > 10}
 <p>{countA} is greater than 10</p>
{:else if countA < 5}
 <p>{count} is less than 5</p>
{:else}
 <p>{countA} is between 0 and 10</p>
{/if}
<h1 style="color: {selectedA}">Pick a colour</h1>
<div>
    {#each colors as color, i}
        <button
            id="color-buttun"
            aria-current={selectedA === color}
            aria-label={color}
            style="background: {color}"
            on:click={() => selectedA = color}
        >{i + 1}</button>
    {/each}

</div>
<button on:click={handleClick}>
	Remove first thing
</button>

{#each things as thing (thing.id)}
	<Thing name={thing.name} />
{/each}

<button on:click={handleClickA}>
	generate random number
</button>

{#await promise}
    <p>...waiting</p>
{:then number}
    <p>The number is {number}</p>
{:catch error}
    <p style="color: red">{error.message}</p>
{/await}

<!-- 1-5.Events -->
<div id="domEvent" on:pointermove={(e) => {
    m = { x: e.clientX, y: e.clientY };
}}>
	The pointer is at {m.x} x {m.y}
</div>

<button on:click|once={() => alert('clicked')}>
	Click me
</button>

<!--<Inner on:message={handleMessage} />-->
<Outer on:message={handleMessage} />

<BigRedButton on:click={handleClickB} />


<!-- 1-6.Binding -->
<input bind:value={nameA}>

<h1>Hello {nameA}!</h1>

<label>
	<input type="number" bind:value={a} min="0" max="10" />
	<input type="range" bind:value={a} min="0" max="10" />
</label>

<label>
	<input type="number" bind:value={b} min="0" max="10" />
	<input type="range" bind:value={b} min="0" max="10" />
</label>

<p>{a} + {b} = {a + b}</p>

<label>
	<input type="checkbox" bind:checked={yes} />
	Yes! Send me regular email spam
</label>

{#if yes}
	<p>
		Thank you. We will bombard your inbox and sell
		your personal details.
	</p>
{:else}
	<p>
		You must opt in to continue. If you're not
		paying, you're the product.
	</p>
{/if}

<button disabled={!yes}>Subscribe</button>

<h2>Insecurity questions</h2>

<form on:submit|preventDefault={handleSubmit}>
	<select
        bind:value={selected}
		on:change={() => (answer = '')}
	>
		{#each questions as question}
			<option value={question}>
				{question.text}
			</option>
		{/each}
	</select>

	<input bind:value={answer} />

	<button disabled={!answer} type="submit">
		Submit
	</button>
</form>

<p>
	selected question {selected
		? selected.id
		: '[waiting...]'}
</p>

<h2>Size</h2>

{#each [1, 2, 3] as number}
	<label>
		<input
			type="radio"
			name="scoops"
			value={number}
            bind:group={scoops}
		/>

		{number} {number === 1 ? 'scoop' : 'scoops'}
	</label>
{/each}

<h2>Flavours</h2>

<select multiple bind:value={flavours}>
	{#each ['cookies and cream', 'mint choc chip', 'raspberry ripple'] as flavour}
		<option>{flavour}</option>
	{/each}
</select>

{#if flavours.length === 0}
	<p>Please select at least one flavour</p>
{:else if flavours.length > scoops}
	<p>Can't order more flavours than scoops!</p>
{:else}
	<p>
		You ordered {scoops} {scoops === 1 ? 'scoop' : 'scoops'}
		of {formatter.format(flavours)}
	</p>
{/if}

<div class="grid">
	input
	<textarea bind:value></textarea>

	output
	<div>{@html marked(value)}</div>
</div>


<style>
    p{
        color: goldenrod;
        font-family: 'Comic Sans MS', cursive;
        font-size: 2em;
    }
    h1 {
		transition: color 0.2s;
	}

	/* div {
		display: grid;
		grid-template-columns: repeat(7, 1fr);
		grid-gap: 5px;
		max-width: 400px;
	} */

	button#color-buttun{
		aspect-ratio: 1;
		border-radius: 50%;
		background: var(--color, #fff);
		transform: translate(-2px,-2px);
		filter: drop-shadow(2px 2px 3px rgba(0,0,0,0.2));
		transition: all 0.1s;
	}

	button#color-buttun[aria-current="true"] {
		transform: none;
		filter: none;
		box-shadow: inset 3px 3px 4px rgba(0,0,0,0.2);
	}

    #domEvent {
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		padding: 1rem;
	}

    .grid {
		display: grid;
		grid-template-columns: 5em 1fr;
		grid-template-rows: 1fr 1fr;
		grid-gap: 1em;
		height: 100%;
	}

	textarea {
		flex: 1;
		resize: none;
	}
</style>