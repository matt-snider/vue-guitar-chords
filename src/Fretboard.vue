<template>
    <svg viewBox="0 0 100 100">
        <!-- Nut and bottom border -->
        <line x1="0" y1="0" x2="100" y2="0"
                stroke="black" stroke-width="3"/>
        <line x1="0" y1="100" x2="100" y2="100"
                stroke="black" stroke-width="0.5"/>


        <!-- Frets -->
        <line x1="0" y1="20" x2="100" y2="20" stroke="black" stroke-width="0.5"/>
        <line x1="0" y1="40" x2="100" y2="40" stroke="black" stroke-width="0.5"/>
        <line x1="0" y1="60" x2="100" y2="60" stroke="black" stroke-width="0.5"/>
        <line x1="0" y1="80" x2="100" y2="80" stroke="black" stroke-width="0.5"/>

        <!-- Finger placement -->
        <slot></slot>
    </svg>
</template>
