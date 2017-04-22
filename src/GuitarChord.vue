<template>
    <svg width="100%" viewBox="0 0 100 100">
        <!-- Chord name -->
        <text x="50" y="8" fill="black" font-size="8" text-anchor="middle">
            {{ chord.name }}
        </text>

        <!-- Tuning -->
        <text v-for="(note, index) in chord.tuning"
            :y="85 - index*13" x="10"
            :transform="`rotate(-90, 10, ${85 - index*13})`"
            fill="black" font-size="8">
            {{ note }}
        </text>

        <text v-if="chord.nut !== 0" x="8" y="108" fill="black" font-size="8" text-anchor="start">
            {{ chord.nut }}
        </text>

        <svg x="10" y="10" width="90" height="80" viewBox="0 0 100 100">
            <!-- Fretboard edges -->
            <line x1="0" y1="0" x2="100" y2="0"
                    stroke="black" stroke-width="1"/>
            <line x1="0" y1="100" x2="100" y2="100"
                    stroke="black" stroke-width="1"/>
            <line x1="100" y1="0" x2="100" y2="100"
                    stroke="black" stroke-width="0.5"/>

            <!-- Nut -->
            <line x1="0" y1="0" x2="0" y2="100"
                    stroke="black" stroke-width="2"/>

            <!-- Frets -->
            <line x1="20" y1="0" x2="20" y2="100" stroke="black" stroke-width="0.5"/>
            <line x1="40" y1="0" x2="40" y2="100" stroke="black" stroke-width="0.5"/>
            <line x1="60" y1="0" x2="60" y2="100" stroke="black" stroke-width="0.5"/>
            <line x1="80" y1="0" x2="80" y2="100" stroke="black" stroke-width="0.5"/>

            <!-- Strings: nested SVGs to make positioning easier -->
            <line stroke="black" stroke-width="0.5" x1="0" y1="7.5" x2="100" y2="7.5"/>
            <line stroke="black" stroke-width="0.5" x1="0" y1="24.5" x2="100" y2="24.5"/>
            <line stroke="black" stroke-width="0.5" x1="0" y1="41.5" x2="100" y2="41.5"/>
            <line stroke="black" stroke-width="0.5" x1="0" y1="58.5" x2="100" y2="58.5"/>
            <line stroke="black" stroke-width="0.5" x1="0" y1="75.5" x2="100" y2="75.5"/>
            <line stroke="black" stroke-width="0.5" x1="0" y1="92.5" x2="100" y2="92.5"/>

            <circle cx="50" cy="42" r="4" stroke="black" stroke-width="3" fill="black" />
            <text x="50" y="44" fill="white" font-size="8" text-anchor="middle">
                1
            </text>
        </svg>
    </svg>
</template>

<script>
const CHORD = {
    name: 'G Chord',
    nut: 0,
    tuning: ['E', 'A', 'D', 'G', 'B', 'e'],
    fingers: [
        {finger: 1, string: 0, fret: 0}
    ],
};

export default {
    data() {
        return {
            chord: CHORD,
        };
    },
};
</script>
