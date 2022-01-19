<script>
	import { spring } from 'svelte/motion';
    import { browser } from "$app/env";

	let coords = spring({ x: 50, y: 50 }, {
		stiffness: 0.1,
		damping: 0.25
	});

	let size = spring(1);

    if (browser) {
        document.documentElement.setAttribute("data-hydrated", "true");
    }
</script>

<svelte:window
    on:mousemove={e => $coords = { x: e.clientX, y: e.clientY }}
	on:mousedown="{() => $size = 4}"
	on:mouseup="{() => $size = 1}"
/>

<div on:mousedown|preventDefault class="cursor-follow" style="--x: {$coords.x}px; --y: {$coords.y}px; --scale: {$size};"></div>

<slot />

<style lang="scss">
    :global {
        :root {
            scroll-behavior: smooth;
            color-scheme: dark;
            font-family: "Manrope", sans-serif;
            --accent: #ff0206;
            --accent-alt: #d80004;
        }

        html, body {
            background-color: #121212;
        }

        body {
            display: flex;
            margin: 0;
            padding: 0;
        }

        *, *::before, *::after {
            box-sizing: border-box;
        }

        ::selection {
            background-color: var(--accent);
            color: #000;
        }
    }

    .cursor-follow {
        transform: translate(calc(var(--x) - 50%), calc(var(--y) - 50%)) scale(var(--scale));
        inline-size: 12px;
        block-size: 12px;
        z-index: 9999;
        pointer-events: none;
        position: fixed;
        border-radius: 50%;
        backdrop-filter: invert(1) grayscale(1);
    }
</style>