<template>
    <svg :x="x" :y="y">
        <finger width="10" height="10" :label="finger"></finger>
    </svg>
</template>

<script>
import Finger from './Finger.vue';

export default {
    components: {
        Finger,
    },
    props: [
        'string',
        'fret',
        'finger',
    ],
    computed: {
        x() {
            return 2.5 + this.string  * 17;
        },

        y() {
            return (this.fret - 1) * 20 + 5;
        },
    },
};
</script>
