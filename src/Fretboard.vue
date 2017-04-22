<template>
    <svg viewBox="0 0 100 100">
        <!-- Fretboard edges -->
        <line x1="0" y1="0" x2="100" y2="0"
                stroke="black" stroke-width="1"/>
        <line x1="0" y1="100" x2="100" y2="100"
                stroke="black" stroke-width="1"/>
        <line x1="100" y1="0" x2="100" y2="100"
                stroke="black" stroke-width="0.5"/>

        <!-- Nut -->
        <line x1="0" y1="0" x2="0" y2="100"
                stroke="black" stroke-width="2"/>

        <!-- Frets -->
        <line x1="20" y1="0" x2="20" y2="100" stroke="black" stroke-width="0.5"/>
        <line x1="40" y1="0" x2="40" y2="100" stroke="black" stroke-width="0.5"/>
        <line x1="60" y1="0" x2="60" y2="100" stroke="black" stroke-width="0.5"/>
        <line x1="80" y1="0" x2="80" y2="100" stroke="black" stroke-width="0.5"/>

        <!-- Strings -->
        <line stroke="black" stroke-width="0.5" x1="0" y1="7.5" x2="100" y2="7.5"/>
        <line stroke="black" stroke-width="0.5" x1="0" y1="24.5" x2="100" y2="24.5"/>
        <line stroke="black" stroke-width="0.5" x1="0" y1="41.5" x2="100" y2="41.5"/>
        <line stroke="black" stroke-width="0.5" x1="0" y1="58.5" x2="100" y2="58.5"/>
        <line stroke="black" stroke-width="0.5" x1="0" y1="75.5" x2="100" y2="75.5"/>
        <line stroke="black" stroke-width="0.5" x1="0" y1="92.5" x2="100" y2="92.5"/>
    </svg>
</template>
