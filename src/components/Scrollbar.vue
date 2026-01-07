<script setup>
import { onMounted, onUnmounted, ref } from 'vue';

const thumbY = ref(0);
const isScollable = ref(false);
const coeff = ref(0);
const scrollTrack = ref()
const scrollThumb = ref()

onMounted(() => {
    const borderWithSum = 0;
    const scrollableScreen = document.getElementById('content');
    const scrollContainer = scrollableScreen.parentElement;
    
    const updateScrollbar = () => {
        isScollable.value = scrollableScreen.clientHeight > scrollContainer.clientHeight;
        if (!isScollable) { return };
        if (!scrollThumb.value) { return }

        const maxScrollScreen = scrollableScreen.scrollHeight - scrollContainer.clientHeight;
        const maxScrollTrack = scrollTrack.value.clientHeight - scrollThumb.value.clientHeight;

        // calulate the coefficient of scrolled pixels
        coeff.value = scrollContainer.scrollTop / (maxScrollScreen + borderWithSum);
        thumbY.value = Math.round(maxScrollTrack * coeff.value);
    }

    updateScrollbar();
    scrollContainer.addEventListener('scroll', updateScrollbar);
    window.addEventListener('resize', updateScrollbar);
})

onUnmounted(() => {
    const scrollContainer = document.getElementById('container').parentElement;
    scrollContainer.removeEventListener('scroll', updateScrollbar);
    window.removeEventListener('resize', updateScrollbar);
})
</script>

<template>
    <div class="absolute top-0 right-0 w-8 h-full z-30 font-rubik py-[3dvw]">
        <div ref="scrollTrack" class="w-full h-full relative flex justify-center">
            <div ref="scrollThumb" v-if="isScollable" :data-scroll-thumb-y="thumbY"
                :style="`top: ${thumbY - 1}px`" class="w-5/8 cursor-pointer bg-neutral-300 absolute top-0 h-10 rounded-xs flex items-center justify-center">
                <span class="text-[12px] text-white rotate-270 text-left leading-none flex items-center justify-center">
                    {{Math.round(coeff * 100)}}
                </span>
            </div>
        </div>
    </div>
</template>