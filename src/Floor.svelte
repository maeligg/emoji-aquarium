<script>
    export let getRandomHorizontalPosition;
    
    const floorOptions = [
        {
        value: ' ',
        weight: 30
        },
        {
        value: '🌾',
        weight: 30
        },
        {
        value: '🌿',
        weight: 30
        },
        {
        value: '🐚',
        weight: 5
        },
        {
          value: '🌱',
          weight: 3
        },
        {
        value: '🥒',
        weight: 3
        },
        {
        value: '⚓',
        weight: 1
        },
        {
        value: '💀',
        weight: 1
        },
        {
        value: '🥾',
        weight: 1
        },
        {
        value: '⭐',
        weight: 1
        }
    ];

    const crawlerOptions = ['🦀', '🦞', '🐌'];
    
    const getRandomFloorTile = () => {
        let optionsArray = [];
        floorOptions.forEach(option => {
        optionsArray.push(...Array(option.weight).fill(option.value));
        });

        return optionsArray[Math.floor(Math.random() * optionsArray.length)];
    };

    let floorSlots;
    const setFloorSlots = () => {
        floorSlots = [...Array(Math.floor(window.innerWidth / 20))].map(slot => getRandomFloorTile())
    };
    setFloorSlots();

    const crawlers = [...Array(Math.floor(Math.random() * 3 + 1))].map(slot => crawlerOptions[Math.floor(Math.random() * crawlerOptions.length)]);
</script>

<svelte:window on:resize={setFloorSlots} />
<div class="floor">
  {#each floorSlots as slot}
    <span class="floor-tile" class:is-plant={slot === '🌾' || slot === '🌿' || slot === '🌱'}>{slot}</span>
  {/each}
  {#each crawlers as crawler}
  <span class="crawler"
    style="
        left: {getRandomHorizontalPosition()};
    "
    class:is-snail={crawler === '🐌'}
  >{crawler}</span>
  {/each}
</div>

<style>
    .floor {
		width: 100%;
		margin-top: auto;
		display: flex;
		font-size: 40px;
	}

	.floor-tile {
		z-index: 1;
		width: 20px;
	}

	.floor-tile.is-plant {
		animation: 2s ease-in-out infinite alternate current;
	}

	@keyframes current {
		0% {
			transform: skewX(0);
		}

		100% {
			transform: skewX(-20deg);
		}
	}

	.crawler {
        position: absolute;
        z-index: 0;
        animation-name: crawl;
        animation-duration: 20s;
        animation-timing-function: steps(30);
        animation-iteration-count: infinite;
        animation-direction: alternate;
    }

	.crawler.is-snail {
        animation-name: swim-left;
        animation-direction: reverse;
        animation-timing-function: linear;
	}

	@keyframes crawl {
		0% {
			transform: translate(0);
		}

		100% {
			transform: translate(-400px);
		}
	}
</style>