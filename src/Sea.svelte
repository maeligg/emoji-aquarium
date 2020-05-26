<script>
    export let getRandomVerticalPosition;
    export let getRandomHorizontalPosition;
  
    const weightedOptions = [
        {
        value: '🐟',
        weight: 10
        },
        {
        value: '🐠',
        weight: 6
        },
        {
        value: '🐡',
        weight: 6
        },
        {
        value: '🦐',
        weight: 3
        },
        {
        value: '🦈',
        weight: 2
        },
        {
        value: '🐬',
        weight: 2
        },
        {
        value: '🐋',
        weight: 1
        },
        {
        value: '🐙',
        weight: 1
        },
        {
        value: '🦑',
        weight: 1
        }
    ];
  
    const getRandomFish = () => {
		let optionsArray = [];
		weightedOptions.forEach(option => {
			optionsArray.push(...Array(option.weight).fill(option.value));
		})

		return optionsArray[Math.floor(Math.random() * optionsArray.length)];
	}

    const getRandomFishSize = () => (Math.random() * 30 + 20 + 'px');

    const getRandomAnimationDuration = () => {
		return Math.random() * 10 + 10  + 's';
	};

    let fishies;
    const setFishies = () => {
        fishies = [...Array((Math.floor(Math.random() * 5)) + 5)].map(slot => getRandomFish());
    }
    setFishies();
</script>

<svelte:window on:resize={setFishies} />
<div class="sea">
  {#each fishies as fish}
    <span
        key={fish}
        class="fish"
        class:swim-right={Math.floor(Math.random() * 2)}
        style="
            top: {getRandomVerticalPosition()};
            left: {getRandomHorizontalPosition()};
            font-size: {getRandomFishSize()};
            animation-duration: {getRandomAnimationDuration()};
        "
    >{fish}</span>
  {/each}
</div>

<style>
    .sea {
        height: 100%;
        overflow: hidden;
	}

	.fish {
        position: absolute;
        animation-name: swim-left;
        animation-timing-function: ease-in-out;
        animation-iteration-count: infinite;
    }

    .fish.swim-right {
        animation-name: swim-right;
    }
</style>
