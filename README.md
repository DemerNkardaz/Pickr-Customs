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
	$("[aria-label='color swatch']").on("dblclick", function() {
		var valueElement = $(".pcr-type.active");
		var inputValue = valueElement.data("type");
		const color =pickr.getColor($(this)[0]);
		if(color) {
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

</details>

### Plans
- Drag&drop swatch for apply color to the object (First steps maked)
- Big swatch pallete (currently WIP JSON contains 227 [Traditional colors of Japan](https://en.wikipedia.org/wiki/Traditional_colors_of_Japan) + tooltips of color names `!WARNING: Using of this JSON will make you pickr loading some laggy on start`
- Ability to add own swatches from pickr to custom palette tab, ability to remove swatch from custom palette `(half-ready, need fixes; ready - add to palette, save palette on localstorage, remove from palette with local storage, bootstrap 5 container with tab)`
- Moveable and resizeable pickr window with JQuery UI and height-resizeable color parameters subwindow
- Options menu with language select, custom palette as TXT column file, some other settings.

<p align="center">
	<h4>Some of tests</h4>
	<img src="https://i.imgur.com/hVDbWer.gif">
</p>


