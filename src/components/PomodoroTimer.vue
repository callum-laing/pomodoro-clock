<script setup>
import { ref, computed } from 'vue';

const timeLeft = ref(1500);
const intervalId = ref(null);
const mode = ref('work');

const timer = computed(() => {
	const minutes = Math.floor(timeLeft.value / 60);
	const seconds = timeLeft.value % 60;
	return `${minutes}:${seconds.toString().padStart(2, '0')}`;
});

const modeLabel = computed(() => {
	return mode.value === 'work' ? 'Work' : 'Take a Break';
});
intervalId.value = setInterval(() => {
	if (timeLeft.value > 0) {
		timeLeft.value--;
	} else {
		if (mode.value === 'work') {
			mode.value = 'break';
			timeLeft.value = 300;
		} else {
			stopTimer();
		}
	}
}, 1000);

function stopTimer() {
	clearInterval(intervalId.value);
}
</script>

<template>
	<div class="timerBox">
		<p class="mode">{{ modeLabel }}</p>
		<p class="timer">{{ timer }}</p>
	</div>
</template>

<style lang="scss" scoped>
.timerBox {
	display: flex;
	align-items: center;
	justify-content: center;
	flex-direction: column;
	font-size: 2em;
}
</style>
