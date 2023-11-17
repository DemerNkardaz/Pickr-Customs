# Pickr-Customs
This is just my trying to customize Pickr with AI using (I'm not a true coder)
<hr><br/><br/><br/>

<h3 align="center">
   <a href="https://github.com/simonwep/pickr">Pickr</a>
</h3>
<p align="center">Link to original repository of Pickr.</p>
<br/><br/><br/><hr>

#### Main dependecies
- Pickr
- Bootstrap 5+
- JQuery 3.7+

- Google Fonts — Material Icons
```css
@import url('https://fonts.googleapis.com/icon?family=Material+Icons');
```

#### Additional dependecies
For dragging & resizes.
- JQuery UI 1.13+

##### Minor dependecies
Is not required, just stylizing my customs.
- Google Fonts — Noto Color Emoji
```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Color+Emoji&display=swap');
```
- Google Fonts — Montserrat
```css
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600&display=swap');
```

#

#### Color Copy
This is mini-additional make you able to copy color from pallete with selected color mode (HEXA/RGA/HSVA/HSLA) to the clipboard.
##### JS
```js
    // "pickr" must be available in code for this, i.e. const pickr = Pickr.create({...)};
    function convertColor(color, inputValue) {
        let roundedColorString = null;
        if (typeof color === "string") {
            color = new pickr.Color(color);
        }
        if (inputValue === "HEXA") {
            roundedColorString = color.toHEXA().toString();
        } else if (inputValue === "RGBA") {
            roundedColorString = "rgba(" + color.toRGBA().map(value => Math.round(value)).join(", ") + ")";
        } else if (inputValue === "CMYK") {
            roundedColorString = "cmyk(" + color.toCMYK().map(value => Math.round(value) + "%").join(", ") + ")";
        } else if (inputValue === "HSLA") {
            roundedColorString = "hsla(" + color.toHSLA().map((value, index) => (index === 1 || index === 2 ? Math.round(value) + "%" : Math.round(value))).join(", ") + ")";
        } else if (inputValue === "HSVA") {
            roundedColorString = "hsva(" + color.toHSVA().map((value, index) => (index === 1 || index === 2 ? Math.round(value) + "%" : Math.round(value))).join(", ") + ")";
        }
        return roundedColorString;
    }
    $("[aria-label='color swatch']").on("dblclick", function () {
        var valueElement = $(".pcr-type.active");
        var inputValue = valueElement.data("type");
        const color = pickr.getColor();
        if (color) {
            let roundedColorString = convertColor(color, inputValue);
            navigator.clipboard.writeText(`${roundedColorString}`);
            $(this).addClass('on_overlay_ofclick');
            setTimeout(() => {
                $(this).removeClass('on_overlay_ofclick');
            }, 1000);
        }
    });
```
##### Style
```css
[aria-label='color swatch'].on_overlay_ofclick {
    --pcr-color: #4082eecc !important;
    z-index: 100;
}
[aria-label='color swatch'].on_overlay_ofclick::after {
    content: '✓' !important;
    font-size: 20px !important;
    color: white;
    line-height: 1.1;
}
```

