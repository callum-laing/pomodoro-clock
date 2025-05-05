<script setup>
import { ref, onMounted } from 'vue';

const isLightMode = ref(false);

onMounted(() => {
	const saved = localStorage.getItem('theme');
	if (saved === 'light') {
		isLightMode.value = true;
		document.documentElement.classList.add('light-mode');
	}
});

function toggleMode() {
	isLightMode.value = !isLightMode.value;

	if (isLightMode.value) {
		document.documentElement.classList.add('light-mode');
		localStorage.setItem('theme', 'light');
	} else {
		document.documentElement.classList.remove('light-mode');
		localStorage.setItem('theme', 'dark');
	}
}
</script>

<template>
	<header>
		<nav>
			<h1>Pomodoro Clock</h1>
			<button @click="toggleMode">{{ isLightMode ? 'Dark' : 'Light' }}</button>
		</nav>
	</header>
</template>

<style lang="scss" scoped>
nav {
	display: flex;
	justify-content: space-between;
	height: 3em;
	border-bottom: 1px solid rgba(60, 60, 60);
	background-color: rgba(40, 40, 40, 0.5);
	margin-bottom: 50px;

	h1 {
		font-size: 1.2em;
		padding: 10px;
	}

	button {
		background-color: transparent;
		margin: 5px;
		padding: 5px 5px;
		border-radius: 10px;
	}
}
</style>
