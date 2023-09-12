<script lang="ts">
	type Counter = {
		count: number;
		title: string;
	};

	let counters: Counter[] = [
		{
			count: 0,
			title: 'new'
		}
	];

	const countUp = (i: number) => (counters[i].count += 1);
	const countDown = (i: number) => counters[i].count > 0 && (counters[i].count -= 1);
	const countReset = (i: number) => (counters[i].count = 0);

	const addCounter = () => (counters = [...counters, { count: 0, title: 'new' }]);
	const removeCounter = (i: number) => (counters = counters.filter((_, index) => index !== i));

	$: titleList = counters.map((counter) => counter.title).join(', ');
	$: totalCount = counters.reduce((prev, current) => prev + current.count, 0);
</script>

<h1 class="text-center text-[64px]">Multiple Counter</h1>
{#each counters as { count }, i}
	<div class="flex justify-center mb-2">
		<div class="h-[43px] w-96 bg-[#F7FAFC]">
			<div class="flex h-full items-center shadow-lg rounded">
				<input type="text" class="text-[#718096] mx-4 px-1 w-32" bind:value={counters[i].title} />
				<span class="text-lg font-bold px-[27px] w-[42px]">{count}</span>
				<div class="ml-auto text-white text-lg">
					<button class="bg-[#F56565] rounded-l h-[35px] w-9" on:click={() => countUp(i)}>+</button><!----><button
						class="bg-[#4299E1] h-[35px] w-[31px]"
						on:click={() => countDown(i)}>-</button
					><!----><button class="bg-[#ECC94B] rounded-r h-[35px] w-[33px]" on:click={() => countReset(i)}>0</button
					><!----><button class="text-[#A0AEC0] text-base px-4" on:click={() => removeCounter(i)}>x</button>
				</div>
			</div>
		</div>
	</div>
{/each}

<div class="flex flex-col items-center">
	<button class="h-6 w-96 bg-[#68D391] rounded" on:click={addCounter}>
		<p class="text-white">new counter</p>
	</button>
	<p>title list: {titleList}</p>
	<p>sum of count: {totalCount}</p>
</div>
