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
This is mini-addition make you able to copy color from pallete with selected color mode (HEXA/RGA/HSVA/HSLA) to the clipboard on double-click to swatch.
<details>
  <summary>See</summary>
<p align="center">
  <img src="https://i.imgur.com/hVDbWer.gif">
</p>

<h4 align="center"><a href="https://demernkardaz.github.io/Pickr-Customs/demo_cc.html" target="_blank">Demo</a></h4>

	
##### JS
```js
    // "pickr" must be available in code for this, i.e. const pickr = Pickr.create({...)};
    function convertColor(color, inputValue) {
        let roundedColorString = null;
        if (typeof color === "string") {
            color = pickr.Color.fromString(color);
        }
        if (inputValue === "HEXA") {
            roundedColorString = color.toHEXA().toString();
        } else if (inputValue === "RGBA") {
            roundedColorString = `rgba(${Math.round(color.toRGBA()[0])}, ${Math.round(color.toRGBA()[1])}, ${Math.round(color.toRGBA()[2])}, ${color.a})`;
        } else if (inputValue === "CMYK") {
            roundedColorString = `cmyk(${Math.round(color.toCMYK()[0])}%, ${Math.round(color.toCMYK()[1])}%, ${Math.round(color.toCMYK()[2])}%, ${Math.round(color.toCMYK()[3])}%)`;
        } else if (inputValue === "HSLA") {
            roundedColorString = `hsla(${Math.round(color.toHSLA()[0])}, ${Math.round(color.toHSLA()[1])}%, ${Math.round(color.toHSLA()[2])}%, ${color.a})`;
        } else if (inputValue === "HSVA") {
            roundedColorString = `hsva(${Math.round(color.toHSVA()[0])}, ${Math.round(color.toHSVA()[1])}%, ${Math.round(color.toHSVA()[2])}%, ${color.a})`;
        }
        return roundedColorString;
    }
    $("[aria-label='color swatch']").on("dblclick", function () {
        var valueElement = $(".pcr-type.active");
        var inputValue = valueElement.data("type");
        const color = pickr.getColor($(this)[0]);
        if (color) {
            let roundedColorString = convertColor(color, inputValue);
            navigator.clipboard.writeText(`${roundedColorString}`);

            if ($(this).hasClass('on_overlay_ofclick')) {
                $(this).removeClass('on_overlay_ofclick')
                clearTimeout(endTimeout);
                setTimeout(() => { $(this).addClass('on_overlay_ofclick'); }, 10);
            } else {
                $(this).addClass('on_overlay_ofclick');
            }
            endTimeout = setTimeout(() => {
                $(this).removeClass('on_overlay_ofclick');
            }, 1400);
        }
    });
```
##### Style
```css
[aria-label='color swatch'].on_overlay_ofclick {
    background: linear-gradient(var(--pcr-color), var(--pcr-color)), url("data:image/svg+xml;utf8, <svg xmlns=\"http://www.w3.org/2000/svg\" viewBox=\"0 0 2 2\"><path fill=\"white\" d=\"M1,0H2V1H1V0ZM0,1H1V2H0V1Z\"/><path fill=\"gray\" d=\"M0,0H1V1H0V0ZM1,1H2V2H1V1Z\"/></svg>") !important;
    background-size: 6px !important;
}

[aria-label='color swatch'].on_overlay_ofclick::before {
    animation: fadeOut 1s ease 0.5s forwards;
}

[aria-label='color swatch'].on_overlay_ofclick::after {
    background-image: url('data:image/svg+xml;utf8, <svg xmlns="http://www.w3.org/2000/svg" enable-background="new 0 0 24 24" height="24" viewBox="0 0 28 26" width="24"><rect fill="none" height="24" width="24"/><path fill="white" d="M22,5.18L10.59,16.6l-4.24-4.24l1.41-1.41l2.83,2.83l10-10L22,5.18z M19.79,10.22C19.92,10.79,20,11.39,20,12 c0,4.42-3.58,8-8,8s-8-3.58-8-8c0-4.42,3.58-8,8-8c1.58,0,3.04,0.46,4.28,1.25l1.44-1.44C16.1,2.67,14.13,2,12,2C6.48,2,2,6.48,2,12 c0,5.52,4.48,10,10,10s10-4.48,10-10c0-1.19-0.22-2.33-0.6-3.39L19.79,10.22z"/><style xmlns="" type="text/css" id="igtranslator-color"/></svg>') !important;
    background-blend-mode: luminosity;
    transition: all 0.5s ease;
    z-index: 100;
    opacity: 0.5;
    animation: fadeOut 1s ease 0.5s forwards;
}

@keyframes fadeOut {

    100% {
        opacity: 0;
        filter: brightness(200%);
    }
}
```

</details>

### Plans
- Drag&drop swatch for apply color to the object (First steps maked)
- Big swatch pallete (currently WIP JSON contains 227 [Traditional colors of Japan](https://en.wikipedia.org/wiki/Traditional_colors_of_Japan) + tooltips of color names `!WARNING: Using of this JSON will make you pickr loading some laggy on start`
- Ability to add own swatches from pickr to custom palette tab, ability to remove swatch from custom palette `(half-ready, need fixes; ready - add to palette, save palette on localstorage, remove from palette with local storage, bootstrap 5 container with tab)`
- Moveable and resizeable pickr window with JQuery UI and height-resizeable color parameters subwindow
- Options menu with language select, custom palette as TXT column file, some other settings.

<h4 align="center">
	Some of tests
</h4>
<p align="center">
	<img src="https://i.imgur.com/go92iyU.gif">
</p>



