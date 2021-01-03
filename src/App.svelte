<script>
  	import Floor from './Floor.svelte';
  	import Sea from './Sea.svelte';

	const getRandomVerticalPosition = () => (Math.floor(Math.random() * (window.innerHeight - 100)) + 'px');
	const getRandomHorizontalPosition = () => {
		let position = Math.floor(Math.random() * (window.innerWidth - 40));
		if (position < 100) position = 100;
		if (position > window.innerWidth - 140) position = window.innerWidth - 140;
		return position + 'px';
	};
</script>

<main>
	<a href="https://github.com/maeligg/emoji-aquarium" class="about-link">
		<svg height="512" width="512" xmlns="http://www.w3.org/2000/svg" fill="#fff" viewBox="0 0 512 512"><path d="M277.332 128c0 11.781-9.55 21.332-21.332 21.332s-21.332-9.55-21.332-21.332 9.55-21.332 21.332-21.332 21.332 9.55 21.332 21.332zm0 0M256 405.332c-8.832 0-16-7.168-16-16V224h-21.332c-8.832 0-16-7.168-16-16s7.168-16 16-16H256c8.832 0 16 7.168 16 16v181.332c0 8.832-7.168 16-16 16zm0 0"/><path d="M256 512C114.836 512 0 397.164 0 256S114.836 0 256 0s256 114.836 256 256-114.836 256-256 256zm0-480C132.48 32 32 132.48 32 256s100.48 224 224 224 224-100.48 224-224S379.52 32 256 32zm0 0"/><path d="M304 405.332h-96c-8.832 0-16-7.168-16-16s7.168-16 16-16h96c8.832 0 16 7.168 16 16s-7.168 16-16 16zm0 0"/></svg>
	</a>
	<Sea getRandomVerticalPosition={getRandomVerticalPosition} getRandomHorizontalPosition={getRandomHorizontalPosition} />
  	<Floor getRandomHorizontalPosition={getRandomHorizontalPosition} />
</main>

<style>
	main {
		position: relative;
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		background: linear-gradient(to bottom, hsl(199, 95%, 59%), hsl(199, 95%, 13%));
		overflow: hidden;
	}

	.about-link {
		position: absolute;
		top: 10px;
		right: 10px;
	}

	.about-link svg {
		width: 30px;
		height: 30px;
	}

	@keyframes -global-swim-left {
		0% {
			transform: translateX(0) scaleX(1);
		}

		45% {
			transform: translateX(-400px) scaleX(1);
		}

		50% {
			transform: translateX(-400px) scaleX(-1);
		}

		95% {
			transform: translateX(0) scaleX(-1);
		}

		100% {
			transform: translateX(0) scaleX(1);
		}
    }
    
    @keyframes -global-swim-right {
		0% {
			transform: translateX(0) scaleX(-1);
		}

		45% {
			transform: translateX(400px) scaleX(-1);
		}

		50% {
			transform: translateX(400px) scaleX(1);
		}

		95% {
			transform: translateX(0) scaleX(1);
		}

		100% {
			transform: translateX(0) scaleX(-1);
		}
	}
</style>