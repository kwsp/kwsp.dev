<script lang="ts">
	import { page } from '$app/stores';

	const isCurrent = (pathname: string, slug: string) => {
		if (slug.length === 0) {
			return pathname === '/';
		}
		return pathname.startsWith(`/${slug}`);
	};

	const navData = [
		{ slug: '', title: 'Home' },
		{ slug: 'projects', title: 'Projects' }
	];
</script>

<header>
	<nav>
		<ul>
			{#each navData as section}
				<li aria-current={isCurrent($page.url.pathname, section.slug) ? 'page' : undefined}>
					<a href="/{section.slug}">{section.title}</a>
				</li>
			{/each}
		</ul>
	</nav>
</header>

<style>
	header {
		display: flex;
		justify-content: space-between;
	}

	nav {
		width: 100%;
		display: flex;
		overflow: auto;
		justify-content: center;
	}

	nav ul {
		position: relative;
		padding: 0;
		margin: 0;
		height: 3em;
		display: flex; /* Always show the menu in a flex layout on non-mobile screens */
		justify-content: center;
		align-items: center;
		list-style: none;
		background-size: contain;
	}

	nav li {
		position: relative;
		height: 100%;
	}

	nav li[aria-current='page']::before {
		--size: 6px;
		content: '';
		width: 0;
		height: 0;
		position: absolute;
		top: 0;
		left: calc(50% - var(--size));
		border: var(--size) solid transparent;
		border-top: var(--size) solid var(--color-theme-1);
	}

	nav a {
		display: flex;
		height: 100%;
		align-items: center;
		padding: 0 0.5rem;
		color: var(--color-text);
		text-decoration: none;
		transition: color 0.2s linear;
	}

	a:hover {
		color: var(--color-theme-1);
	}
</style>
