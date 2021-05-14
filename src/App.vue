<template>
	<div class="min-h-full grid grid-layout bg-white dark:bg-[#1d1d1d]">
		<Navbar />
		<div>
			<router-view />
		</div>
		<Footer />
	</div>
</template>

<script setup lang="ts">
import Navbar from '~/components/Navbar.vue';

import { useStore } from './store';

const store = useStore();

const checkDarkMode = () => {
	const persistedColorPreference = window.localStorage.getItem('theme');
	const hasPersistedPreference = typeof persistedColorPreference === 'string';
	if (hasPersistedPreference) {
		return persistedColorPreference === 'dark';
	}
	const mql = window.matchMedia('(prefers-color-scheme: dark)');
	const hasMediaQueryPreference = typeof mql.matches === 'boolean';
	if (hasMediaQueryPreference) {
		return mql.matches;
	}
	return false;
};
const addDarkModeSelector = () => {
	if (checkDarkMode()) {
		document.documentElement.classList.add('dark');
		store.commit({
			type: 'setDarkMode',
			darkMode: true,
		});
	} else {
		document.documentElement.classList.remove('dark');
		store.commit({
			type: 'setDarkMode',
			darkMode: false,
		});
	}
};
const watchDarkMode = () => window.matchMedia('(prefers-color-scheme: dark)').addListener(addDarkModeSelector);
watchDarkMode();
addDarkModeSelector();
void store.dispatch('fetchStats');
</script>

<style>
.grid-layout {
	grid-template-rows: auto 1fr auto;
}
</style>
