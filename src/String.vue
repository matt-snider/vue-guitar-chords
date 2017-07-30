<template>
    <line stroke="black" stroke-width="0.5" class="string"
        :x1="x" y1="0" :x2="x" y2="100"/>
</template>

<script>
export default {
    props: ['i'],
    computed: {
        x() {
            return 20 * this.i;
        },
    },
};
</script>

