<template>
    <svg :width="width" :height="height">
        <svg preserveAspectRatio="none"
            viewBox="0 0 100 100">
            <rect width="100%" height="100%" rx="5" ry="50"
                fill="black" stroke="black"/>
        </svg>
        <finger :x="this.width/2 - 5" y="0" width="10" height="10"
            :label="label"/>
    </svg>
</template>

<script>
import Finger from './Finger.vue';

export default {
    components: {
        Finger,
    },
    props: [
        'label',
        'width',
        'height',
    ],
};
</script>
