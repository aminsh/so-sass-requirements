# Sass-Requirements
Do your best in sass using this lightweight package.

<img src="https://nodei.co/npm/sass-requirements.png" />

## Using this predefined requirements
If your sass compiler knows how to use npm packages, it's enough to import this package like this:
```scss
@import "sass-requirements";
```
Otherwise add `npm_modules` in `includePaths` (In [node-sass](https://www.npmjs.com/package/node-sass))
or `load_paths` (In [official sass](http://sasscss.org/1))
argument of your sass config.

## Functions
### `strip-unit`
Simply strips the unit e.g. converts `1px` to `1`.

Usage:
```scss
element{
    width: 100cm + 100px; // 102.64583cm
    width: strip-unit(100cm) + 100px; // 200px
    width: 100px + 100cm; // 3879.52755906px
    width: strip-unit(100px) + 100cm; // 200cm
}
```

## Mixin List
It's obvious that what should we use is for making a specific thing
cross-browser.
* Backgrounds
  * `bg($color)`
  * `bg-color($color)`
  * `bg-size($size)`
  * `bg-img($value)`
  * `gradient($adjustment, $dir: top, $default-bg: "", $gradient-mode: linear)`
      For example:
      ```scss
      element{
          @include gradient(
              "#{$color-black}, #{$color-white}",// adjustment
              top,
              $color-black,
              linear
          );
      }
      ```
      equals to:
      ```css
      element{
          background: #303030;
          background-image: -webkit-linear-gradient(top ,#303030, #ffffff);
          background-image: -o-linear-gradient(top,#303030, #ffffff);
          background-image: -moz-linear-gradient(top,#303030, #ffffff);
          background-image: linear-gradient(to bottom,#303030, #ffffff);
      }
      ```
* Borders
  * `border($mode [,$value])` e.g.
    ```scss
    element{
      @include border(top, 1px solid $color-black);
    }
    ```
    equals to
    ```css
    element{
      border-top: 1px solid #303030;
    }
    ```
    and this:
    ```scss
    element{
      @include border(1px solid $color-black);
    }
    ```
    equals to:
    ```css
    element{
      border: 1px solid #303030;
    }
    ```
  * `border-radius($value: 0.2rem)`
* Transitions
  * `transition($value: inherit)`
  * `trans` abbr.
  * `transition-duration($duration: inherit)`
    * `trans-dur` abbr.
  * `transition-property($properties: inherit)`
    * `trans-prop` abbr.
  * `transition-delay($delay: inherit)`
    * `trans-dly` abbr.
  * `transition-timing-function($timingFn: inherit)`
    * `trans-time-fn` abbr.
* Transforms
  * `transform($transforms: inherit)`
    * `transform-origin($value: center center)`
* Shadows
  * `box-shadow($shadow: 0px 1px 2px 1px rgba(0,0,0,0.2))`
  * `text-shadow($shadow)`
* Margins
  * `margin-v($value)`
  * `margin-h($value)`
* Paddings
  * `padding-v($value)`
  * `padding-h($value)`
* Animations
  * `anim($value)`
  * `anim-name($name: inherit)`
  * `anim-delay($delay)`
    * `anim-dly($delay)` abbr.
  * `anim-duration($duration)`
    * `anim-dur` abbr.
  * `anim-timing-function($timingFn)`
    * `anim-timing-func` abbr.
    * `anim-time-fn` abbr.
  * `anim-fill-mode($mode: inherit)`
  * `keyframes($animName){ @content }`
    Makes cross browser keyframes, e.g.
    ```scss
    @include keyframes(myKeyframes){
        from{ color: black }
        to  { color: white }
    }
    ```
    equals to:
    ```css
    @keyframes myKeyframes{
        from{ color: black }
        to  { color: white }
    }
    @-o-keyframes myKeyframes{
        from{ color: black }
        to  { color: white }
    }
    @-ms-keyframes myKeyframes{
        from{ color: black }
        to  { color: white }
    }
    @-moz-keyframes myKeyframes{
        from{ color: black }
        to  { color: white }
    }
    @-khtml-keyframes myKeyframes{
        from{ color: black }
        to  { color: white }
    }
    @-webkit-keyframes myKeyframes{
        from{ color: black }
        to  { color: white }
    }
    ```
* Overflows
  * `overflow-x($value: hidden)`
  * `overflow-y($value: hidden)`
* Others
  * `box-sizing($size)`
  * `dir($direction)`
  * `no-user-select()`
    Prevents highlighting that specific element, e.g.
    ```scss
    textarea{
        @include no-user-select();
    }
    ```
    equals to:
    ```css
    textarea{
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
    }
    ```
  * `no-focus-outline()`
    Prevents outlines to be visible when user focuses on a specific element, e.g.
    ```scss
    element{
        @include no-focus-outline();
    }
    ```
    equals to:
    ```css
    element:focus{
        outline: 0 !important;
    }
    element::-moz-focus-inner{
        border: 0; 
    }
    ```
  * `perspective($value: 0)`
  * `backface-visib($value)` (( abbreviation of backface-visibility ))
  * `text-stroke($fg-color, $stroke-color: "")`
    Makes something similar to text stroke by using text-shadow property.
  * `word-break()`
    equals to this:
    ```css
    element{
        white-space: pre-wrap;
        word-break: break-all;
        word-wrap: break-word;
    }
    ```
  * `placeholder(){ @content }`
  * `filter($value)`
  * `selection($selection){ @content }`
    Makes cross-browser selection styles, e.g.
    ```scss
    @include selection(element){
        color: white;
        background-color: rgba(0,0,255,0.5);    
    }
    ```
    equals to:
    ```css
    element::selection{
        color: white;
        background-color: rgba(0,0,255,0.5);
    }
    element::-moz-selection{
        color: white;
        background-color: rgba(0,0,255,0.5);
    }
    ```

## Color List
The colors are predefined for you to make your work nicer.
If you wanna develop this package, the color definitions are like this:
```scss
$color-white: #ffffff;
$color-milk-white: #ecf0f1;
$color-gray-milk-white: #bdc3c7;
$color-gray: #95a5a6;
$color-dark-gray: #7f8c8d;
$color-red: #FF6C5C;
$color-light-red: lighten($color-red, 10);
$color-dark-red: darken($color-red, 25);
$color-white-yellow: #FDE3A7;
$color-yellow: #ffcf4b;
$color-orange: #f39c12;
$color-magenta: #ea4c88;
$color-light-pink: #ff8cc8;
$color-pink: #ff6ca8;
$color-dark-pink: #da3c78;
$color-light-cream: #ffdcb5;
$color-cream: #ffb28b;
$color-dark-cream: #ff926b;
$color-light-brown: #9e6c4b;
$color-brown: #7e4c2b;
$color-dark-brown: #5e2c0b;
$color-light-blue: #39d5ff;
$color-blue: #3498db;
$color-dark-blue: #004790;
$color-cyan-green: #1abc9c;
$color-dark-cyan-green: #16a085;
$color-light-green: #5efca1;
$color-green: #3edc81;
$color-dark-green: #1ebc61;
$color-light-purple: #BE90D4;
$color-purple: #ab69c6;
$color-dark-purple: #8E44AD;
$color-dark-gray-blue: #34495e;
$color-too-dark-gray: #2c3e50;
$color-light-black: #404040;
$color-black: #303030;
$color-real-black: #000000;

// Thanks to www.flatuicolorpicker.com ( Since v1.0.5 )
$color-cinnabar: #f03434;
$color-soft-red: #EC644B;
$color-chestnut-rose: #D24D57;
$color-pomegranate: #F22613;
$color-thunderbird: #D91E18;
$color-old-brick: #96281B;
$color-flamingo: #EF4836;
$color-valencia: #D64541;
$color-tall-poppy: #C0392B;
$color-monza: #CF000F;
$color-cinnabar: #E74C3C;
$color-razzmatazz: #DB0A5B;
$color-sunset-orange: #F64747;
$color-wax-flower: #F1A9A0;
$color-cabaret: #D2527F;
$color-new-york-pink: #E08283;
$color-radical-red: #F62459;
$color-sunglo: #E26A6A;
$color-lavender-purple: #947CB0;
$color-snuff: #DCC6E0;
$color-rebeccapurple: #663399;
$color-honey-flower: #674172;
$color-wistful: #AEA8D3;
$color-plum: #913D88;
$color-seance: #9A12B3;
$color-medium-purple: #BF55EC;
$color-light-wisteria: #BE90D4;
$color-studio: #8E44AD;
$color-wisteria: #9B59B6;
$color-sherpa-blue: #013243;
$color-san-marino: #446CB3;
$color-alice-blue: #E4F1FE;
$color-royal-blue: #4183D7;
$color-picton-blue: #59ABE3;
$color-spray: #81CFE0;
$color-shakespeare: #52B3D9;
$color-humming-bird: #C5EFF7;
$color-picton-blue: #22A7F0;
$color-curious-blue: #3498DB;
$color-madison: #2C3E50;
$color-dodger-blue: #19B5FE;
$color-ming: #336E7B;
$color-ebony-clay: #22313F;
$color-malibu: #6BB9F0;
$color-summer-sky: #1E8BC3;
$color-chambray: #3A539B;
$color-pickled-bluewood: #34495E;
$color-hoki: #67809F;
$color-jelly-bean: #2574A9;
$color-jacksons-purple: #1F3A93;
$color-jordy-blue: #89C4F4;
$color-steel-blue: #4B77BE;
$color-fountain-blue: #5C97BF;
$color-malachite: #00e640;
$color-summer-green: #91b496;
$color-medium-turquoise: #4ECDC4;
$color-aqua-island: #A2DED0;
$color-gossip: #87D37C;
$color-dark-sea-green: #90C695;
$color-eucalyptus: #26A65B;
$color-caribbean-green: #03C9A9;
$color-silver-tree: #68C3A3;
$color-downy: #65C6BB;
$color-mountain-meadow: #1BBC9B;
$color-light-sea-green: #1BA39C;
$color-medium-aquamarine: #66CC99;
$color-turquoise: #36D7B7;
$color-madang: #C8F7C5;
$color-riptide: #86E2D5;
$color-shamrock: #2ECC71;
$color-niagara: #16a085;
$color-emerald: #3FC380;
$color-green-haze: #019875;
$color-free-speech-aquamarine: #03A678;
$color-ocean-green: #4DAF7C;
$color-niagara-1: #2ABB9B;
$color-jade: #00B16A;
$color-salem: #1E824C;
$color-observatory: #049372;
$color-jungle-green: #26C281;
$color-saffron-mango: #fabe58;
$color-confetti: #e9d460;
$color-cape-honey: #FDE3A7;
$color-california: #F89406;
$color-fire-bush: #EB9532;
$color-tahiti-gold: #E87E04;
$color-casablanca: #F4B350;
$color-crusta: #F2784B;
$color-sea-buckthorn: #EB974E;
$color-lightning-yellow: #F5AB35;
$color-burnt-orange: #D35400;
$color-buttercup: #F39C12;
$color-ecstasy: #F9690E;
$color-sandstorm: #F9BF3B;
$color-jaffa: #F27935;
$color-zest: #E67E22;
$color-white-smoke: #ececec;
$color-lynch: #6C7A89;
$color-pumice: #D2D7D3;
$color-gallery: #EEEEEE;
$color-silver-sand: #BDC3C7;
$color-silversand: #BDC3C7; // because of old usages
$color-porcelain: #ECF0F1;
$color-cascade: #95A5A6;
$color-iron: #DADFE1;
$color-edward: #ABB7B7;
$color-cararra: #F2F1EF;
$color-silver: #BFBFBF;

$color-bronze: #CD7F32;

$color-map: (
        color-white: #ffffff,
        color-milk-white: #ecf0f1,
        color-gray-milk-white: #bdc3c7,
        color-gray: #95a5a6,
        color-dark-gray: #7f8c8d,
        color-red: #FF6C5C,
        color-light-red: lighten($color-red, 10),
        color-dark-red: darken($color-red, 25),
        color-white-yellow: #FDE3A7,
        color-yellow: #ffcf4b,
        color-orange: #f39c12,
        color-magenta: #ea4c88,
        color-light-pink: #ff8cc8,
        color-pink: #ff6ca8,
        color-dark-pink: #da3c78,
        color-light-cream: #ffdcb5,
        color-cream: #ffb28b,
        color-dark-cream: #ff926b,
        color-light-brown: #9e6c4b,
        color-brown: #7e4c2b,
        color-dark-brown: #5e2c0b,
        color-light-blue: #39d5ff,
        color-blue: #3498db,
        color-dark-blue: #004790,
        color-cyan-green: #1abc9c,
        color-dark-cyan-green: #16a085,
        color-light-green: #5efca1,
        color-green: #3edc81,
        color-dark-green: #1ebc61,
        color-light-purple: #BE90D4,
        color-purple: #ab69c6,
        color-dark-purple: #8E44AD,
        color-dark-gray-blue: #34495e,
        color-too-dark-gray: #2c3e50,
        color-light-black: #404040,
        color-black: #303030,
        color-real-black: #000000,

        // Thanks to www.flatuicolorpicker.com ( Since v1.0.5 )
        color-cinnabar: #f03434,
        color-soft-red: #EC644B,
        color-chestnut-rose: #D24D57,
        color-pomegranate: #F22613,
        color-thunderbird: #D91E18,
        color-old-brick: #96281B,
        color-flamingo: #EF4836,
        color-valencia: #D64541,
        color-tall-poppy: #C0392B,
        color-monza: #CF000F,
        color-cinnabar: #E74C3C,
        color-razzmatazz: #DB0A5B,
        color-sunset-orange: #F64747,
        color-wax-flower: #F1A9A0,
        color-cabaret: #D2527F,
        color-new-york-pink: #E08283,
        color-radical-red: #F62459,
        color-sunglo: #E26A6A,
        color-lavender-purple: #947CB0,
        color-snuff: #DCC6E0,
        color-rebeccapurple: #663399,
        color-honey-flower: #674172,
        color-wistful: #AEA8D3,
        color-plum: #913D88,
        color-seance: #9A12B3,
        color-medium-purple: #BF55EC,
        color-light-wisteria: #BE90D4,
        color-studio: #8E44AD,
        color-wisteria: #9B59B6,
        color-sherpa-blue: #013243,
        color-san-marino: #446CB3,
        color-alice-blue: #E4F1FE,
        color-royal-blue: #4183D7,
        color-picton-blue: #59ABE3,
        color-spray: #81CFE0,
        color-shakespeare: #52B3D9,
        color-humming-bird: #C5EFF7,
        color-picton-blue: #22A7F0,
        color-curious-blue: #3498DB,
        color-madison: #2C3E50,
        color-dodger-blue: #19B5FE,
        color-ming: #336E7B,
        color-ebony-clay: #22313F,
        color-malibu: #6BB9F0,
        color-summer-sky: #1E8BC3,
        color-chambray: #3A539B,
        color-pickled-bluewood: #34495E,
        color-hoki: #67809F,
        color-jelly-bean: #2574A9,
        color-jacksons-purple: #1F3A93,
        color-jordy-blue: #89C4F4,
        color-steel-blue: #4B77BE,
        color-fountain-blue: #5C97BF,
        color-malachite: #00e640,
        color-summer-green: #91b496,
        color-medium-turquoise: #4ECDC4,
        color-aqua-island: #A2DED0,
        color-gossip: #87D37C,
        color-dark-sea-green: #90C695,
        color-eucalyptus: #26A65B,
        color-caribbean-green: #03C9A9,
        color-silver-tree: #68C3A3,
        color-downy: #65C6BB,
        color-mountain-meadow: #1BBC9B,
        color-light-sea-green: #1BA39C,
        color-medium-aquamarine: #66CC99,
        color-turquoise: #36D7B7,
        color-madang: #C8F7C5,
        color-riptide: #86E2D5,
        color-shamrock: #2ECC71,
        color-niagara: #16a085,
        color-emerald: #3FC380,
        color-green-haze: #019875,
        color-free-speech-aquamarine: #03A678,
        color-ocean-green: #4DAF7C,
        color-niagara-1: #2ABB9B,
        color-jade: #00B16A,
        color-salem: #1E824C,
        color-observatory: #049372,
        color-jungle-green: #26C281,
        color-saffron-mango: #fabe58,
        color-confetti: #e9d460,
        color-cape-honey: #FDE3A7,
        color-california: #F89406,
        color-fire-bush: #EB9532,
        color-tahiti-gold: #E87E04,
        color-casablanca: #F4B350,
        color-crusta: #F2784B,
        color-sea-buckthorn: #EB974E,
        color-lightning-yellow: #F5AB35,
        color-burnt-orange: #D35400,
        color-buttercup: #F39C12,
        color-ecstasy: #F9690E,
        color-sandstorm: #F9BF3B,
        color-jaffa: #F27935,
        color-zest: #E67E22,
        color-white-smoke: #ececec,
        color-lynch: #6C7A89,
        color-pumice: #D2D7D3,
        color-gallery: #EEEEEE,
        color-silver-sand: #BDC3C7,
        color-silversand: #BDC3C7, // because of old usage
        color-porcelain: #ECF0F1,
        color-cascade: #95A5A6,
        color-iron: #DADFE1,
        color-edward: #ABB7B7,
        color-cararra: #F2F1EF,
        color-silver: #BFBFBF,

        color-bronze: #CD7F32
);
```

###### ♥ Thank You for Using ♥
***
###### Thanks to [css-tricks.com](https://css-tricks.com/)