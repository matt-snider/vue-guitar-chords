<template>
    <svg width="100%" viewBox="0 0 100 100">
        <fretboard x="0" y="0" width="100" height="100"
            @stringClicked="stringClicked">
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

let selected;
let strings = new Map();

export default {
    components: {
        Fretboard,
        FrettedNote,
    },
    data() {
        return {
            fretted: [],
        };
    },
    methods: {
        stringClicked(event) {
            if (!strings.has(event.string)) {
                let newFretted = {
                    string: event.string,
                    fret: event.fret,
                    finger: 1,
                };
                this.fretted.push(newFretted);
                strings.set(event.string, newFretted);
            } else {
                strings.get(event.string).fret = event.fret;
            }
        },
    },
};
</script>
