<template>
    <svg width="100%" viewBox="0 0 100 100"
        tabindex="0"
        @keyup.esc="remove"
        @keyup.delete="remove"
        @keyup.up="moveFret(-1)"
        @keyup.down="moveFret(1)"
        @keyup.left="moveString(-1)"
        @keyup.right="moveString(1)"
        @keyup.fingers="setFinger">
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
import Vue from 'vue';
import Fretboard from './Fretboard.vue';
import FrettedNote from './FrettedNote.vue';

let selected;

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
            let newFretted = this.fretted.find(x => x.string === event.string);
            if (!newFretted) {
                newFretted = {
                    string: event.string,
                    fret: event.fret,
                    finger: 1,
                };
                this.fretted.push(newFretted);
            }
            selected = newFretted;
        },

        moveFret(change) {
            if (!selected) {
                return;
            }
            let newValue = selected.fret + change;
            if (newValue >= 1 && newValue <= 5) {
                selected.fret = newValue;
            }
        },

        moveString(change) {
            if (!selected) {
                return;
            }
            let newValue = selected.string + change;
            if (newValue >= 0 && newValue <= 5) {
                selected.string = newValue;
            }
        },

        remove() {
            if (!selected) {
                return;
            }
            let index = this.fretted.findIndex(x => x === selected);
            this.fretted.splice(index, 1);
            selected = null;
        },

        setFinger(event) {
            if (!selected) {
                return;
            }
            selected.finger = event.key;
        },
    },

    beforeCreate() {
        // Register 1, 2, 3, 4 as fingerings
        // Note: need numpad too (96,...)
        Vue.config.keyCodes = {
            fingers: [49, 50, 51, 52, 97, 98, 99, 100],
        };
    },
};
</script>
