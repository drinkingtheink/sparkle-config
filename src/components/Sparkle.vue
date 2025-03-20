<template>
    <svg id="sparkle" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 201.67 193.55">
        <path
            :style="{ 'animation-delay': lrgStarDelay + 's', 'animation-duration': animationDuration + 's' }"
            id="lrg-star"
            class="cls-1"
            d="M99.63,68.77l17.31,6.4c2.61.97,2.61,4.66,0,5.63l-15.97,5.91c-14.88,5.51-25.85,18.32-28.98,33.88l-9.59,47.57c-.65,3.21-5.23,3.21-5.88,0l-9.59-47.57c-3.14-15.55-14.1-28.37-28.98-33.88l-15.97-5.91c-2.61-.97-2.61-4.66,0-5.63l17.31-6.4c14.15-5.23,24.8-17.1,28.49-31.73L56.54,2.27c.76-3.02,5.05-3.02,5.82,0l8.78,34.78c3.69,14.62,14.35,26.49,28.49,31.73Z"
        />
        <path
            :style="{ 'animation-delay': smlStarDelay + 's', 'animation-duration': animationDuration + 's' }"
            id="sml-star"
            class="cls-1"
            d="M194.34,43.53l6.59,2.44c.99.37.99,1.77,0,2.14l-6.08,2.25c-5.66,2.1-9.84,6.97-11.03,12.89l-3.65,18.1c-.25,1.22-1.99,1.22-2.24,0l-3.65-18.1c-1.19-5.92-5.37-10.8-11.03-12.89l-6.08-2.25c-.99-.37-.99-1.77,0-2.14l6.59-2.44c5.38-1.99,9.44-6.51,10.84-12.07l3.34-13.23c.29-1.15,1.92-1.15,2.21,0l3.34,13.23c1.4,5.57,5.46,10.08,10.84,12.07Z"
        />
        <path
            :style="{ 'animation-delay': medStarDelay + 's', 'animation-duration': animationDuration + 's' }"
            id="med-star"
            class="cls-1"
            d="M178.33,137.39l9.55,3.53c1.44.53,1.44,2.57,0,3.1l-8.81,3.26c-8.21,3.04-14.26,10.11-15.99,18.69l-5.29,26.24c-.36,1.77-2.89,1.77-3.24,0l-5.29-26.24c-1.73-8.58-7.78-15.65-15.99-18.69l-8.81-3.26c-1.44-.53-1.44-2.57,0-3.1l9.55-3.53c7.8-2.89,13.68-9.43,15.72-17.5l4.84-19.18c.42-1.67,2.79-1.67,3.21,0l4.84,19.18c2.04,8.07,7.92,14.61,15.72,17.5Z"
        />
    </svg>
</template>

<script>
export default {
  name: 'SparkleImg',
  props: {
    smlStarDelay: Number,
    medStarDelay: Number,
    lrgStarDelay: Number,
    animationDuration: Number,
  }
}
</script>

<style>
:root {
    --bluefill: #17a5ff;
}

.cls-1 {
    fill: var(--bluefill);
    stroke-width: 0px;
    transition: all 1s;
    fill: initial;
}

#sparkle {
    overflow: visible;
}

#lrg-star,
#med-star,
#sml-star {
    animation-name: twinkle;
    animation-iteration-count: infinite;
    transform-origin: center;
}

@keyframes twinkle {
    0% {
        fill: var(--bluefill);
    }
    10% {
        fill: gray;
        transform: scale(0.95);
    }
    30% {
        fill: gray;
        transform: scale(1.05);
    }
    50% {
        fill: var(--bluefill);
        transform: scale(1);
    }
    100% {
        fill: var(--bluefill);
    }
}
</style>