<template>
    <svg width="100%" viewBox="0 0 110 110">
        <!-- Borders - left/right -->
        <line x1="10" y1="10" x2="100" y2="10"
                stroke="black" stroke-width="1"/>
        <line x1="10" y1="99" x2="100" y2="99"
                stroke="black" stroke-width="1"/>

        <!-- Borders - bottom/top -->
        <line x1="10" y1="10" x2="10" y2="100"
                stroke="black" stroke-width="3"/>
        <line x1="100" y1="10" x2="100" y2="100"
                stroke="black" stroke-width="0.5"/>

        <!-- Strings -->
        <line v-for="s in strings" stroke="black" stroke-width="0.5"
            :x1="s.x1" :y1="s.y1" :x2="s.x2" :y2="s.y2"/>

        <!-- Fingers -->
        <circle cx="50" cy="48" r="4" stroke="black" stroke-width="3" fill="black" />
        <text x="50" y="50" fill="white" font-size="8" text-anchor="middle">
            1
        </text>


        <!-- Nut position -->
        <text v-if="chord.nut !== 0" x="8" y="108" fill="black" font-size="8" text-anchor="start">
            {{ chord.nut }}
        </text>

        <!-- Tuning -->
        <text v-for="(note, index) in chord.tuning"
            :y="95 - index*16" x="6"
            :transform="`rotate(-90,6, ${95 - index*16})`"
            fill="black" font-size="8">
            {{ note }}
        </text>

        <!-- Chord name -->
        <text x="50" y="8" fill="black" font-size="8" text-anchor="middle">
            {{ chord.name }}
        </text>
        Sorry, your browser does not support inline SVG.
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

// 16 between strings
// 5 between string and fretboard edge
const STRINGS = [
    {x1: 10, y1: 15, x2: 100, y2: 15},

    {x1: 10, y1: 31, x2: 100, y2: 31},
    {x1: 10, y1: 47, x2: 100, y2: 47},
    {x1: 10, y1: 63, x2: 100, y2: 63},
    {x1: 10, y1: 79, x2: 100, y2: 79},

    {x1: 10, y1: 95, x2: 100, y2: 95},
];

export default {
    data() {
        return {
            chord: CHORD,
            strings: STRINGS,
        };
    },
};
</script>
