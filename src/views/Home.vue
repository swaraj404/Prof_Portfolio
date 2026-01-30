<script setup>
import { ref, onMounted } from 'vue';
import TextAnim from '@/components/TextAnim.vue'
import FramedMainSection from '@/layouts/FramedMainSection.vue';

const frameRef = ref(null);
const containerRef = ref(null);

onMounted(() => {
    containerRef.value = frameRef.value.sectionRef;
});
</script>

<template>
    <FramedMainSection ref="frameRef" id="swaraj" class="h-dvh">
        <div 
            class="h-full w-full bg-fit bg-cover bg-position-[center_40%] rounded-4xl bg-[url('/backgrounds/mountains.jpg')] flex flex-col justify-center items-center text-center">
            <div
                class="text-[#fff] font-rubik uppercase text-[10dvw] xl:text-[13dvh] leading-none flex flex-col justify-center items-center w-full">
                <p class="flex h-[8.4dvw] xl:h-[11dvh] overflow-hidden w-full justify-center ml-[20dvw] xl:ml-[20dvh] gap-4">
                    <span class="standard-text">Turning</span>
                    <TextAnim 
                        v-if="containerRef"
                        :texts="['Ideas', 'Code', 'Data', 'Problems', 'Dreams']" 
                        :container="containerRef" 
                        :duration="2.5" 
                        :class="'text-red-custom'" 
                    />
                </p>
                <p class="flex h-[8.4dvw] xl:h-[11dvh] ">into</p>
                <p class="flex h-[8.4dvw] xl:h-[11dvh] ">innovative</p>
                <p class="flex h-[8.4dvw] xl:h-[11dvh] ">solutions</p>
            </div>
        </div>
    </FramedMainSection>
</template>
