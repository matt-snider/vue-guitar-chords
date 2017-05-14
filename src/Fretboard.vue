<template>
    <svg viewBox="0 0 100 100" ref="svg">
        <!-- Fretboard edges -->
        <line x1="0" y1="0" x2="0" y2="100"
                stroke="black" stroke-width="1"/>
        <line x1="100" y1="0" x2="100" y2="100"
                stroke="black" stroke-width="1"/>
        <line x1="0" y1="100" x2="100" y2="100"
                stroke="black" stroke-width="0.5"/>

        <!-- Nut -->
        <line x1="0" y1="0" x2="100" y2="0"
                stroke="black" stroke-width="3"/>

        <!-- Frets -->
        <line x1="0" y1="20" x2="100" y2="20" stroke="black" stroke-width="0.5"/>
        <line x1="0" y1="40" x2="100" y2="40" stroke="black" stroke-width="0.5"/>
        <line x1="0" y1="60" x2="100" y2="60" stroke="black" stroke-width="0.5"/>
        <line x1="0" y1="80" x2="100" y2="80" stroke="black" stroke-width="0.5"/>

        <!-- Strings -->
        <line v-for="i in [0, 1, 2, 3, 4, 5]"
            @click="stringClicked(i, $event)"
            stroke="black" stroke-width="0.5" :class="'string-' + i"
            :x1="7.5 + 17*i" y1="0" :x2="7.5 + 17*i" y2="100"/>

        <!-- Finger placement -->
        <slot></slot>
    </svg>
</template>

<script>
let svgPoint;

export default {
    methods: {
        fretFromClick(event) {
            svgPoint.x = event.clientX;
            svgPoint.y = event.clientY;

            let inversePt = this.$refs.svg.getScreenCTM().inverse()
            let svgClick = svgPoint.matrixTransform(inversePt);
            return Math.floor(1 + svgClick.y / 20);
        },

        stringClicked(string, event) {
            let fret = this.fretFromClick(event);
            this.$emit('stringClicked', { string, fret });
        },
    },

    mounted() {
        svgPoint = this.$refs.svg.createSVGPoint();
    },
};
</script>

<style>
.string-0:hover,
.string-1:hover,
.string-2:hover,
.string-3:hover,
.string-4:hover,
.string-5:hover {
    stroke: grey;
    stroke-width: 2;
}
.string-0:hover ~ .fretted-note-0 circle,
.string-1:hover ~ .fretted-note-1 circle,
.string-2:hover ~ .fretted-note-2 circle,
.string-3:hover ~ .fretted-note-3 circle,
.string-4:hover ~ .fretted-note-4 circle,
.string-5:hover ~ .fretted-note-5 circle
.string:hover ~ .fretted-note {
    fill: grey;
}

.fretted-note-0 circle:hover,
.fretted-note-1 circle:hover,
.fretted-note-2 circle:hover,
.fretted-note-3 circle:hover,
.fretted-note-4 circle:hover,
.fretted-note-5 circle:hover {
    fill: grey;
}

.fretted-note-0.active circle,
.fretted-note-1.active circle,
.fretted-note-2.active circle,
.fretted-note-3.active circle,
.fretted-note-4.active circle,
.fretted-note-5.active circle {
    fill: blue !important;
}
</style>
