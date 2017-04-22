<template>
    <div id="app">
        <h1> Vue Guitar Chords </h1>
        <div style="width:250px; height:250px;">
            <guitar-chord></guitar-chord>
        </div>
    </div>
</template>

<script>
import GuitarChord from './GuitarChord.vue';

export default {
    components: {
        GuitarChord,
    },
};
</script>
