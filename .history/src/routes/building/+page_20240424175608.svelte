<script lang="ts">
	import blakeSrc from '$lib/assets/blake.jpg?w=200';
	import blakeSrcsetWebp from '$lib/assets/blake.jpg?w=400;200&format=webp&as=srcset';
	import blakeSrcset from '$lib/assets/blake.jpg?w=400;200&as=srcset';
	import riverSrc from '$lib/assets/river.jpg?w=200';
	import riverSrcsetWebp from '$lib/assets/river.jpg?w=400;200&format=webp&as=srcset';
	import riverSrcset from '$lib/assets/river.jpg?w=400;200&as=srcset';
	import Card from '$lib/components/Card.svelte';
	import SpeakerPicture from '$lib/components/SpeakerPicture.svelte';
	import talks from '$lib/data/talks.json';
	import { theme } from '$lib/shared/stores/theme';
	import '$lib/styles/styles.css';
	import { summerTheme } from '$lib/styles/themes/summerTheme.css';
	import { winterTheme } from '$lib/styles/themes/winterTheme.css';
	import '@fontsource/source-sans-pro/400.css';
	import '@fontsource/source-serif-pro/400.css';
	import { abstractText, button, dateText, heading, main, speakerName } from './index-styles.css';

	const sources = [blakeSrc, riverSrc];
	const sourceSets = [blakeSrcset, riverSrcset];
	const sourceSetsWebp = [blakeSrcsetWebp, riverSrcsetWebp];

	$: themeIsSummer = $theme === 'summer';
	$: currentTheme = themeIsSummer ? summerTheme : winterTheme;
	$: abstractTextStyle = `${abstractText} ${currentTheme}`;
	$: buttonStyle = `${button} ${currentTheme}`;
	$: mainStyle = `${main} ${themeIsSummer ? summerTheme : winterTheme}`;
	$: currentIndex = 0;
	$: alt = `Picture of ${talks[currentIndex].speaker}`;
	$: placeholder = talks[currentIndex].profileImageBase64;
	$: src = sources[currentIndex];
	$: srcset = sourceSets[currentIndex];
	$: srcsetWebp = sourceSetsWebp[currentIndex];
</script>

<svelte:head>
	<title>SvelteKit Vanilla Extract: Course Registration Example</title>
</svelte:head>
{#key currentIndex}
	<!-- svelte-ignore component-name-lowercase -->
	<main class={mainStyle}>
		<Card>
			<h1 class={heading}>{talks[currentIndex].title}</h1>
			<SpeakerPicture {alt} {src} {srcset} {srcsetWebp} {placeholder} />
			<div class={speakerName}>{talks[currentIndex].speaker}</div>
			<div class={abstractTextStyle}>{talks[currentIndex].abstract}</div>
			<div class={dateText}>{talks[currentIndex].date}</div>
			<!-- svelte-ignore component-name-lowercase -->
			<button class={buttonStyle} type="button"> Book now!</button>
		</Card>
	</main>
{/key}
