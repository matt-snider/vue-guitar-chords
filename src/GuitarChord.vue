<template>
    <svg width="100%" viewBox="0 0 100 100">
        <!-- Chord name -->
        <text x="50" y="8" fill="black" font-size="8" text-anchor="middle">
            {{ name }}
        </text>

        <!-- Tuning -->
        <text v-for="(note, index) in tuning"
            :y="85 - index*13" x="10"
            :transform="`rotate(-90, 10, ${85 - index*13})`"
            fill="black" font-size="8">
            {{ note }}
        </text>

        <!-- Nut label -->
        <text x="13" y="98" fill="black" font-size="8" text-anchor="start">
            {{ nutPosition }}
        </text>

        <!-- Fretboard and strings -->
        <fretboard x="10" y="10" width="90" height="80">
            <fretted-note v-for="note in fretted"
                :string="note.string"
                :fret="note.fret"
                :finger="note.finger">
            </fretted-note>
        </fretboard>
    </svg>
</template>

<script>
import Fretboard from './Fretboard.vue';
import FrettedNote from './FrettedNote.vue';

export default {
    components: {
        Fretboard,
        FrettedNote,
    },
    props: [
        'name',
        'tuning',
        'fretted',
        'nutPosition',
    ],
};
</script>
