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
                :finger="note.finger"
                :class="[{active: selected===note}, 'fretted-note-' + note.string]"
                @click="stringClicked(note)">
            </fretted-note>
        </fretboard>
    </svg>
</template>

<script>
import Vue from 'vue';
import Fretboard from './Fretboard.vue';
import FrettedNote from './FrettedNote.vue';

export default {
    components: {
        Fretboard,
        FrettedNote,
    },
    data() {
        return {
            fretted: [],
            selected: null,
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
            this.selected = newFretted;
        },

        moveFret(change) {
            if (!this.selected) {
                return;
            }
            let newValue = this.selected.fret + change;
            if (newValue >= 1 && newValue <= 5) {
                this.selected.fret = newValue;
            }
        },

        moveString(change) {
            if (!this.selected) {
                return;
            }
            let newValue = this.selected.string + change;
            if (newValue >= 0 && newValue <= 5) {
                this.selected.string = newValue;
            }
        },

        remove() {
            if (!this.selected) {
                return;
            }
            let index = this.fretted.findIndex(x => x === this.selected);
            this.fretted.splice(index, 1);
            this.selected = null;
        },

        setFinger(event) {
            if (!this.selected) {
                return;
            }
            this.selected.finger = event.key;
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
