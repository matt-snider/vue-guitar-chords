<template>
    <div id="app">
        <h1> Vue Guitar Chords </h1>

        <hr>

        <h2> Chord Diagrams </h2>
        <p class="section-description">
            The following shows how to construct simple chord diagrams with the <code>&lt;GuitarChord/&gt;</code> component.
        </p>
        <div class="chord-container">
            <GuitarChord
                 name="G chord"
                 nut-position="0"
                 tuning="EADGBE"
                 :fretted="[
                    { string: 0, fret: 3, finger: 2 },
                    { string: 1, fret: 2, finger: 1 },
                    { string: 4, fret: 3, finger: 3 },
                    { string: 5, fret: 3, finger: 4 },
                 ]"
            />

            <pre>
            <code>
            &lt;GuitarChord
                name="G chord" 
                nut-position="0"
                tuning="EADGBE"
                :fretted="[
                    { string: 0, fret: 3, finger: 2 },
                    { string: 1, fret: 2, finger: 1 },
                    { string: 4, fret: 3, finger: 3 },
                    { string: 5, fret: 3, finger: 4 },
                ]"
            /&gt;
            </code>
            </pre>
        </div>
        <div class="chord-container">
            <GuitarChord
                 name="A chord"
                 nut-position="0"
                 tuning="EADGBE"
                 :fretted="[{
                    string: [2, 3, 4],
                    fret: 2,
                    finger: 1,
                 }]"
             />

            <pre>
            <code>
            &lt;GuitarChord
                 name="A chord"
                 nut-position="0"
                 tuning="EADGBE"
                 :fretted="[{
                     string: [2, 3, 4],
                     fret: 2,
                     finger: 1,
                 }]"
             /&gt;
            </code>
            </pre>
        </div>


        <h2> Chord Diagram Editor </h2>
        <p class="section-description">
            Diagrams can be edited with the <code>&lt;GuitarChordEditor/&gt;</code> component:
            <ul>
                <li>Press a string and fret position to add a marker</li>
                <li>Click or use the up/down arrow keys to change the fret position</li>
                <li>Use the number keys to change the finger marking (1-4)</li>
                <li>Press the <code>delete</code> key to remove it</li>
            </ul>
        </p>
        <div class="chord-container">
            <GuitarChordEditor/>
        </div>
    </div>
</template>

<script>
import GuitarChord from '../src/GuitarChord.vue';
import GuitarChordEditor from '../src/GuitarChordEditor.vue';

export default {
    components: {
        GuitarChord,
        GuitarChordEditor,
    },
};
</script>

<style>
.section-description {
    margin-bottom: 50px;
}

.chord-container {
    display: inline-block;
    width: 350px;
    height: auto;
    vertical-align: top;

    margin-right: 30px;
}

body {
    margin-bottom: 20px;
}
</style>
