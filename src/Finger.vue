<template>
    <svg viewBox="0 0 100 100">
        <circle cx="50" cy="50" r="49" stroke="black" fill="black"/>
        <text x="50" y="64" fill="white"
            font-size="60" font-weight="bold"
            text-anchor="middle">
            {{ label }}
        </text>
    </svg>
</template>

<script>
export default {
    props: [
        'label',
    ],
};
</script>
