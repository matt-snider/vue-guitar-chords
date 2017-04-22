# vue-guitar-chords

> Guitar Chord Diagrams in VueJS
Provides an SVG-backed component to create guitar chord diagrams.

e.g.
```html
<guitar-chord name="G chord" nut-position="0"
        tuning="EADGBE" :fretted="gChordNotes">
</guitar-chord>
```

Produces:
![G-Chord](http://rawgithub.com/matt-snider/6bbdae922572843aff491579cf3bdd61/raw/0dfc630d63f7c376ec6b4e85a24f794f4e1a2d94/g-chord.svg)

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).
