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
                <fretted-note  v-for="note in findByString(i)"
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
            frettedNotes: [],
            selected: null,
            name: 'X chord',
            tuning: 'EADGBE',
            nutPosition: 0,
        };
    },
    methods: {
        noteClicked(note) {
            console.log('noteClicked', note);
            this.selected = note;
        },

        // When an empty string is clicked, create a note at that position.
        // If the string isn't empty, but sits below a barred note, also create
        // a note at that position.
        // Otherwise, there is a (non-barred) note above or below, and we should
        // simply move it to this new position.
        stringClicked(clickedString, event) {
            let clickedFret = this.fretFromClick(event);
            let closestNote = this.findClosestNote(clickedString, clickedFret);
            console.log('stringClicked', clickedString);
            console.log('clickedFret', clickedFret);
            console.log('closestNote' + ((closestNote && Array.isArray(closestNote.string)) ? ' (barred)' : ''), closestNote);

            if (!closestNote || (closestNote && Array.isArray(closestNote.string) && closestNote.fret < clickedFret)) {
                let newNote = {
                    string: clickedString,
                    fret: clickedFret,
                    finger: 1,
                };
                this.frettedNotes.splice(clickedString, 0, newNote);
                this.selected = newNote;
            } else {
                this.$set(closestNote, 'fret', clickedFret);
                this.selected = closestNote;
            }
        },

        fretFromClick(event) {
            svgPoint.x = event.clientX;
            svgPoint.y = event.clientY;

            let inversePt = svg.getScreenCTM().inverse()
            let svgClick = svgPoint.matrixTransform(inversePt);
            return Math.floor(1 + (svgClick.y - START_Y) / FRET_HEIGHT);
        },

        // Find the closest fretted note to the position given.
        // TODO: rename this -- it doesn't find the closest but rather, the
        // next non-barred note, if it above a barred note, otherwise the barred
        // note itself
        findClosestNote(string, fret) {
            let found;
            let notesOnString = this.findByString(string);
            let simpleNote = notesOnString.find(x => !Array.isArray(x.string));
            if (simpleNote) {
                found = simpleNote;
            } else {
                found = notesOnString[0];
            }
            return found;
        },

        findByString(string) {
            return this.frettedNotes.filter(x =>
                Array.isArray(x.string)
                    ? x.string.includes(string)
                    : x.string === string
            );
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
            this.fretted.splice(this.selected.string, 1);
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
            return this.frettedNotes;
        },
    },

    watch: {
        frettedNotes: {
            handler() {
                let barmap = {};
                for (let [i, f] of this.frettedNotes.entries()) {
                    if (!f) continue;
                    let key = [f.fret, f.finger];
                    if (key in barmap) {
                        let other = barmap[key];
                        other.string = Array.from(new Set([].concat(other.string, f.string))).sort();
                        this.frettedNotes.splice(i, 1);
                    } else {
                        barmap[key] = f;
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
