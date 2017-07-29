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
            <g :class="[{active: selected === fretted[i]}, 'string-group']"
                v-for="i in [0, 1, 2, 3, 4, 5]" :key="i">
                <string @click.native="stringClicked(i, $event)" :i="i"></string>
                <fretted-note v-if="fretted[i]"
                    :string="fretted[i].string"
                    :fret="fretted[i].fret"
                    :finger="fretted[i].finger"
                    class="fretted-note"
                    @click.native="stringClicked(i, $event)">
                </fretted-note>
            </g>
        </base-chord>
        Chord Name: <input type="text" v-model="name"/>
        Tuning:     <input type="text" v-model="tuning"/>
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
            fretted: new Array(6),
            selected: null,
            name: 'X chord',
            tuning: 'EADGBE',
            nutPosition: 0,
        };
    },
    methods: {
        stringClicked(string, event) {
            let fret = this.fretFromClick(event);
            let newFretted = this.fretted[string];
            console.log('click', string, fret);
            if (!newFretted) {
                newFretted = {
                    string,
                    fret,
                    finger: 1,
                };
                this.fretted[string] = newFretted;
            }
            this.selected = newFretted;
        },

        fretFromClick(event) {
            svgPoint.x = event.clientX;
            svgPoint.y = event.clientY;

            let inversePt = svg.getScreenCTM().inverse()
            let svgClick = svgPoint.matrixTransform(inversePt);
            return Math.floor(1 + (svgClick.y - START_Y) / FRET_HEIGHT);
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
