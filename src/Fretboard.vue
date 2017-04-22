<template>
    <svg viewBox="0 0 100 100">
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
        <line stroke="black" stroke-width="0.5" x1="7.5" y1="0" x2="7.5" y2="100"/>
        <line stroke="black" stroke-width="0.5" x1="24.5" y1="0" x2="24.5" y2="100"/>
        <line stroke="black" stroke-width="0.5" x1="41.5" y1="0" x2="41.5" y2="100"/>
        <line stroke="black" stroke-width="0.5" x1="58.5" y1="0" x2="58.5" y2="100"/>
        <line stroke="black" stroke-width="0.5" x1="75.5" y1="0" x2="75.5" y2="100"/>
        <line stroke="black" stroke-width="0.5" x1="92.5" y1="0" x2="92.5" y2="100"/>

        <!-- Finger placement -->
        <slot></slot>
    </svg>
</template>
