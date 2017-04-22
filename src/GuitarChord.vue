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

        <!-- Nut label -->
        <text x="13" y="98" fill="black" font-size="8" text-anchor="start">
            {{ chord.nut }}
        </text>

        <!-- Fretboard and strings -->
        <fretboard x="10" y="10" width="90" height="80">
            <fretted-note v-for="note in chord.fretted"
                :string="note.string"
                :fret="note.fret"
                :finger="note.finger">
            </fretted-note>
        </fretboard>
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

import Fretboard from './Fretboard.vue';
import FrettedNote from './FrettedNote.vue';

export default {
    components: {
        Fretboard,
        FrettedNote,
    },
    data() {
        return {
            chord: CHORD,
        };
    },
};
</script>
