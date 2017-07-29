<template>
    <svg :x="x" :y="y">
        <barred-finger v-if="isBar" :label="finger"
            :width="16 * string.length" height="10"/>
        <finger v-else width="10" height="10" :label="finger"/>
    </svg>
</template>

<script>
import BarredFinger from './BarredFinger.vue';
import Finger from './Finger.vue';

export default {
    components: {
        BarredFinger,
        Finger,
    },
    props: [
        'string',
        'fret',
        'finger',
    ],
    computed: {
        isBar() {
            return Array.isArray(this.string);
        },

        x () {
            let string = this.isBar
                ? this.string[0]
                : this.string;
            return 2.5 + string * 17;
        },

        y () {
            return (this.fret - 1) * 20 + 5;
        },
    },
};
</script>
