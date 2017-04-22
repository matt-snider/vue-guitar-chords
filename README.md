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


<img src="https://rawgit.com/matt-snider/6bbdae922572843aff491579cf3bdd61/raw/a7ac0e411a56d54c41b7a74dc5578a6e3a929de2/g-chord.svg" width="250" height="250"/>

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
