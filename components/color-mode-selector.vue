<template>
    <div class="flex space-x-2 items-center">
        <div class="text-gray-500 text-sm" v-if="showNextModeLabel">Change to {{ nextColorMode }}</div>
        <button 
            @click="setNextColorMode()"
            @mouseenter="showNextModeLabel = true"
            @mouseleave="showNextModeLabel = false"
            class="hover:bg-gray-100 dark:hover:bg-gray-600 px-2 py-1 text-gray-500"
        >
            {{ nextModeIcons[nextColorMode] }}
        </button>
    </div>
</template>

<script setup>
const colorMode = useColorMode();
const showNextModeLabel = ref(false);

const modes  = [
    'system',
    'light',
    'dark'
];

const nextModeIcons = {
    system: '🌓',
    light: '🌕',
    dark: '🌑'
}

const nextColorMode = computed(() => {
    const currentModeIndex = modes.indexOf(colorMode.preference);
    let nextModeIndex = currentModeIndex + 1;
    if (nextModeIndex > modes.length -1) {
        nextModeIndex = 0;
    }
    return modes[nextModeIndex];
});

function setNextColorMode() {
    colorMode.preference = nextColorMode.value
}
</script>