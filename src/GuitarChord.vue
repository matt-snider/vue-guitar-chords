<template>
    <base-chord :name="name" :tuning="tuning"
        :nut-position="nutPosition">
        <string v-for="i in [0, 1, 2, 3, 4, 5]" :i="i"></string>
        <fretted-note v-for="note in fretted"
            :string="note.string"
            :fret="note.fret"
            :finger="note.finger">
        </fretted-note>
    </base-chord>
</template>

<script>
import BaseChord from './BaseChord.vue';
import Fretboard from './Fretboard.vue';
import FrettedNote from './FrettedNote.vue';
import String from './String.vue';

export default {
    components: {
        BaseChord,
        Fretboard,
        FrettedNote,
        String,
    },
    props: [
        'name',
        'tuning',
        'fretted',
        'nutPosition',
    ],
};
</script>
