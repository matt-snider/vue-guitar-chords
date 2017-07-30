<template>
    <div>
        <base-chord :name="name" :tuning="tuning"
            :nut-position="nutPosition"
            ref="svg" tabindex="0"
            @keyup.native.esc="remove"
            @keyup.native.delete="remove"
            @keyup.native.up="moveFret(-1)"
            @keyup.native.down="moveFret(1)"
            @keyup.native.fingers="setFinger">
            <g v-for="i in [0, 1, 2, 3, 4, 5]" :key="i"
                :class="[{active: selected && selected.string === i}, 'string-group']">
                <string @click.native="stringClicked(i, $event)" :i="i"></string>
                <fretted-note  v-for="note in frettedNotes[i]"
                    :key="[note.fret, note.string]"
                    :string="note.string"
                    :fret="note.fret"
                    :finger="note.finger"
                    class="fretted-note"
                    @click.native="noteClicked(note)">
                </fretted-note>
            </g>
        </base-chord>
        Chord Name: <input type="text" v-model="name"/>
        Tuning:     <input type="text" v-model="tuning"/>
        Output: {{jsonOutput }}
    </div>
</template>

<script>
import Vue from 'vue';
import BaseChord from './BaseChord.vue';
import Fretboard from './Fretboard.vue';
import FrettedNote from './FrettedNote.vue';
import String from './String.vue';

let svg;
let svgPoint;
let START_Y = 20;
let FRET_HEIGHT = 20 * 0.8;


export default {
    components: {
        BaseChord,
        Fretboard,
        FrettedNote,
        String,
    },
    data() {
        return {
            frettedNotes: Array.of([], [], [], [], [], []),
            selected: null,
            name: 'X chord',
            tuning: 'EADGBE',
            nutPosition: 0,
        };
    },
    methods: {
        noteClicked(note) {
            this.selected = note;
        },

        // When an empty string is clicked, create a note at that position.
        // If the string isn't empty, but sits below a barred note, also create
        // a note at that position.
        // Otherwise, there is a (non-barred) note above or below, and we should
        // simply move it to this new position.
        stringClicked(clickedString, event) {
            let clickedFret = this.fretFromClick(event);
            let notes = this.frettedNotes[clickedString];
            let simpleNote = this.findSimpleNote(notes);
            let barredNote = this.findBarredNote(notes);
            if(!notes.length || (barredNote && barredNote.fret < clickedFret)) {
                let newNote = {
                    string: clickedString,
                    fret: clickedFret,
                    finger: 1,
                };
                notes.splice(clickedFret, 0, newNote);
                this.selected = newNote;
            } else {
                this.$set(simpleNote, 'fret', clickedFret);
                this.selected = simpleNote;
            }
        },

        fretFromClick(event) {
            svgPoint.x = event.clientX;
            svgPoint.y = event.clientY;

            let inversePt = svg.getScreenCTM().inverse()
            let svgClick = svgPoint.matrixTransform(inversePt);
            return Math.floor(1 + (svgClick.y - START_Y) / FRET_HEIGHT);
        },

        findSimpleNote(notes) {
            return notes.find(x => !Array.isArray(x.string));
        },

        findBarredNote(notes) {
            return notes.find(x => Array.isArray(x.string));
        },

        moveFret(change) {
            if (!this.selected) {
                return;
            }
            let newValue = this.selected.fret + change;
            if (newValue >= 1 && newValue <= 5) {
                this.$set(this.selected, 'fret', newValue);
            }
        },

        remove() {
            if (!this.selected) {
                return;
            }
            let string = Array.isArray(this.selected.string)
                ? this.selected.string[0]
                : this.selected.string;
            let notes = this.frettedNotes[string];
            let updatedNotes = notes.filter(x => x !== this.selected);
            this.$set(this.frettedNotes, string, updatedNotes);
            this.selected = null;
        },

        setFinger(event) {
            if (!this.selected) {
                return;
            }
            this.$set(this.selected, 'finger', event.key);
        },
    },

    computed: {
        jsonOutput() {
            return [].concat(...this.frettedNotes);
        },
    },

    watch: {
        frettedNotes: {
            handler() {
                let map = {};
                for (let notes of this.frettedNotes) {
                    for (let [i, note] of notes.entries()) {
                        let key = [note.fret, note.finger];
                        let other = map[key];
                        if (other && isNeighbour(note, other)) {
                            other.string = uniqueArray(other.string, note.string);
                            notes.splice(i, 1);
                            this.selected = other;
                        } else {
                            // Store key and reference to string array
                            map[key] = note;
                        }
                    }
                }
            },
            deep: true,
        },
    },

    beforeCreate() {
        // Register 1, 2, 3, 4 as fingerings
        // Note: need numpad too (96,...)
        Vue.config.keyCodes = {
            fingers: [49, 50, 51, 52, 97, 98, 99, 100],
        };
    },

    mounted() {
        svg = this.$refs.svg.$el;
        svgPoint = svg.createSVGPoint();
    },
};

function uniqueArray(...items) {
    return Array.from(
        new Set([]
            .concat(...items)
            .sort()
        )
    );
}

function isNeighbour(noteA, noteB) {
    let A = [].concat(noteA.string);
    let B = [].concat(noteB.string);
    let result = false;
    for (let a of A) {
        for (let b of B) {
            if (Math.abs(a - b) === 1) {
                result = true;
                break;
            }
        }
    }
    return result;
}
</script>

<style>
.string-group:hover .string,
.string-group:hover .fretted-note circle {
    stroke-width: 2;
    stroke-opacity: 0.5;
    fill-opacity: 0.7;
}

.string-group.active .string,
.string-group.active .fretted-note circle {
    stroke-width: 2;
    stroke-opacity: 0.5;
    fill-opacity: 0.7;
    fill: blue;
    stroke: blue;
}
</style>
