<script setup>
import Timer from './components/PomodoroTimer.vue';
</script>

<template>
	<header>
		<h1>Pomodoro Clock</h1>
		<Timer />
	</header>
</template>

<style scoped>
body {
	max-height: 100dvh;
}

h1 {
	font-size: 3rem;
	text-align: center;
	padding: 25px 0;
}
</style>
