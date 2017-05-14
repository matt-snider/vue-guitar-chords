<template>
    <svg width="100%" viewBox="0 0 100 100">
        <!-- Chord name -->
        <text y="8" x="50" fill="black"
            font-size="10" font-weight="bold"
            text-anchor="middle">
            {{ name }}
        </text>

        <!-- Tuning -->
        <text v-for="(note, index) in splitTuning"
            :x="15 + index*14" y="18"
            fill="black" font-size="8">
            {{ note }}
        </text>

        <!-- Nut label -->
        <text x="2" y="24"  fill="black" font-size="8">
            {{ nutPosition }}
        </text>

        <!-- Fretboard and strings -->
        <fretboard x="5" y="20" width="95" height="80">
            <slot></slot>
        </fretboard>
    </svg>
</template>

<script>
import Fretboard from './Fretboard.vue';


export default {
    components: {
        Fretboard,
    },
    props: [
        'name',
        'tuning',
        'nutPosition',
    ],
    computed: {
        splitTuning() {
            const re = /[ABCDEFG][#b]?/g;
            let tuning = [];
            let match;
            do {
                match = re.exec(this.tuning);
                if (match) {
                    tuning.push(match[0]);
                }
            } while (match && tuning.length < 6)
            return tuning;
        },
    },
};
</script>
