<script lang="ts">
	import { browser } from '$app/environment';
	import { theme } from '$lib/shared/stores/theme';
	import '$lib/styles/styles.css';
	import { summerTheme } from '$lib/styles/themes/summerTheme.css';
	import { winterTheme } from '$lib/styles/themes/winterTheme.css';
	import lazyload from 'vanilla-lazyload';
	import { container, containerMain, header, themeButton } from './layout-styles.css';
	import { goto } from '$app/navigation';

	if (browser && !document.lazyloadInstance) {
		document.lazyloadInstance = new lazyload();
	}

	$: themeIsSummer = $theme === 'summer';
	$: currentTheme = themeIsSummer ? summerTheme : winterTheme;
	$: buttonText = themeIsSummer ? 'Summer theme' : 'Winter theme';
	$: buttonAriaLabel = themeIsSummer ? 'Switch to Winter theme' : 'Switch to Summer theme';
	$: buttonStyle = `${themeButton} ${currentTheme}`;
</script>

<div class={`${container} ${containerMain} ${currentTheme}`}>
	<!-- svelte-ignore component-name-lowercase -->
	<header class={header}>
		<button
			aria-label={buttonAriaLabel}
			class={buttonStyle}
			on:click={() => ($theme === 'summer' ? theme.set('winter') : theme.set('summer'))}
			>1 {buttonText}</button
		>
		<button
			aria-label={buttonAriaLabel}
			class={buttonStyle}
			on:click={() => ($theme === 'summer' ? theme.set('winter') : theme.set('summer'))}
			>moving</button
		>
		<button aria-label={buttonAriaLabel} class={buttonStyle} on:click={() => goto('/building')}
			>building</button
		>
	</header>
	<slot />
</div>
