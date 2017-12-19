<template>
    <div id="app">
        <h1> Vue Guitar Chords </h1>
        <div style="width:250px; height:250px;">
            <guitar-chord name="G chord" nut-position="0"
                    tuning="EADGBE" :fretted="gChordNotes">
            </guitar-chord>
        </div>

        <div style="width:250px; height:250px;">
            <guitar-chord name="A chord" nut-position="0"
                    tuning="EADGBE" :fretted="aChordNotes">
            </guitar-chord>
        </div>


        <h3> Guitar Chord Editor </h3>
        <div style="width:250px; height:250px;">
            <guitar-chord-editor>
            </guitar-chord-editor>
        </div>
    </div>
</template>

<script>
import GuitarChord from './GuitarChord.vue';
import GuitarChordEditor from './GuitarChordEditor.vue';

export default {
    components: {
        GuitarChord,
        GuitarChordEditor,
    },
    data() {
        return {
            gChordNotes: [
                { string: 0, fret: 3, finger: 2 },
                { string: 1, fret: 2, finger: 1 },
                { string: 4, fret: 3, finger: 3 },
                { string: 5, fret: 3, finger: 4 },
            ],
            aChordNotes: [
                { string: [2, 3, 4], fret: 2, finger: 1 },
            ],
        };
    },
};
</script>
