<script setup>
import { ref, computed } from 'vue';

const timeLeft = ref(1500);
const intervalId = ref(null);
const mode = ref('work');
const isRunning = ref(false);

const timer = computed(() => {
	const minutes = Math.floor(timeLeft.value / 60);
	const seconds = timeLeft.value % 60;
	return `${minutes}:${seconds.toString().padStart(2, '0')}`;
});

const modeLabel = computed(() => {
	return mode.value === 'work' ? 'Time to focus!' : 'Time for a break!';
});

function startTimer() {
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
}

function toggleTimer() {
	if (isRunning.value) {
		stopTimer();
		isRunning.value = false;
	} else {
		startTimer();
		isRunning.value = true;
	}
}

function stopTimer() {
	clearInterval(intervalId.value);
}

function resetTimer() {
	clearInterval(intervalId.value);
	isRunning.value = false;
	timeLeft.value = 1500;
	mode.value = 'work';
}
</script>

<template>
	<div class="timerBox">
		<p class="mode">{{ modeLabel }}</p>
		<p class="timer">{{ timer }}</p>
		<button @click="toggleTimer">{{ isRunning ? 'Pause' : 'Start' }}</button>
		<button v-if="isRunning" @click="resetTimer">Reset</button>
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

.timerBox .timer {
	font-size: 4em;
}
</style>
