<template>
    <svg width="100%" viewBox="0 0 100 100">
        <!-- Chord name -->
        <text y="8" x="50" fill="black"
            font-size="10" font-weight="bold"
            text-anchor="middle">
            {{ name }}
        </text>

        <!-- Tuning -->
        <text v-for="(note, index) in tuning"
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
