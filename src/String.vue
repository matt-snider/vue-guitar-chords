<template>
    <line stroke="black" stroke-width="0.5" class="string"
        :x1="7.5 + 17*i" y1="0" :x2="7.5 + 17*i" y2="100"/>
</template>

<script>
export default {
    props: ['i'],
};
</script>

