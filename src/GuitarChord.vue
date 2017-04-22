<template>
    <svg width="100%" viewBox="0 0 110 110">
        <!-- Fretboard edges -->
        <line x1="10" y1="10" x2="100" y2="10"
                stroke="black" stroke-width="1"/>
        <line x1="10" y1="99" x2="100" y2="99"
                stroke="black" stroke-width="1"/>
        <line x1="100" y1="10" x2="100" y2="100"
                stroke="black" stroke-width="1"/>

        <!-- Nut -->
        <line x1="10" y1="10" x2="10" y2="100"
                stroke="black" stroke-width="2"/>
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

        <!-- Frets -->
        <line x1="28" y1="10" x2="28" y2="100" stroke="black" stroke-width="0.5"/>
        <line x1="46" y1="10" x2="46" y2="100" stroke="black" stroke-width="0.5"/>
        <line x1="64" y1="10" x2="64" y2="100" stroke="black" stroke-width="0.5"/>
        <line x1="82" y1="10" x2="82" y2="100" stroke="black" stroke-width="0.5"/>

        <!-- Strings: nested SVGs to make positioning easier -->
        <line stroke="black" stroke-width="0.5" x1="10" y1="15" x2="100" y2="15"/>
        <line stroke="black" stroke-width="0.5" x1="10" y1="31" x2="100" y2="31"/>
        <line stroke="black" stroke-width="0.5" x1="10" y1="47" x2="100" y2="47"/>
        <line stroke="black" stroke-width="0.5" x1="10" y1="63" x2="100" y2="63"/>
        <line stroke="black" stroke-width="0.5" x1="10" y1="79" x2="100" y2="79"/>
        <line stroke="black" stroke-width="0.5" x1="10" y1="95" x2="100" y2="95"/>

        <circle cx="55" cy="48" r="4" stroke="black" stroke-width="3" fill="black" />
        <text x="55" y="50" fill="white" font-size="8" text-anchor="middle">
            1
        </text>

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
