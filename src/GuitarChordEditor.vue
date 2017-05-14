<template>
    <svg width="100%" viewBox="0 0 100 100" tabindex="0" ref="svg"
        @keyup.esc="remove"
        @keyup.delete="remove"
        @keyup.up="moveFret(-1)"
        @keyup.down="moveFret(1)"
        @keyup.fingers="setFinger">
        <fretboard x="0" y="0" width="100" height="100">
            <g :class="[{active: selected === fretted[i]}, 'string-group']"
                v-for="i in [0, 1, 2, 3, 4, 5]">
                <line @click="stringClicked(i, $event)"
                    stroke="black" stroke-width="0.5" class="string"
                    :x1="7.5 + 17*i" y1="0" :x2="7.5 + 17*i" y2="100"/>
                <fretted-note v-if="fretted[i]"
                    :string="fretted[i].string"
                    :fret="fretted[i].fret"
                    :finger="fretted[i].finger"
                    class="fretted-note"
                    @click="stringClicked(i, $event)">
                </fretted-note>
            </g>
        </fretboard>
    </svg>
</template>

<script>
import Vue from 'vue';
import Fretboard from './Fretboard.vue';
import FrettedNote from './FrettedNote.vue';
let svgPoint;


export default {
    components: {
        Fretboard,
        FrettedNote,
    },
    data() {
        return {
            fretted: new Array(6),
            selected: null,
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
                this.fretted.splice(string, 0, newFretted);
            }
            this.selected = newFretted;
        },

        fretFromClick(event) {
            svgPoint.x = event.clientX;
            svgPoint.y = event.clientY;

            let inversePt = this.$refs.svg.getScreenCTM().inverse()
            let svgClick = svgPoint.matrixTransform(inversePt);
            return Math.floor(1 + svgClick.y / 20);
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
        svgPoint = this.$refs.svg.createSVGPoint();
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
