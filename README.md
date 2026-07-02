# Focus Style

## What is Focus Style?

FS is a simple, lightweight and adaptable CSS starter kit for building web frontends. It is the essence of many years of experience in building website frontends from scratch, both from a designer’s and a developer’s perspective. Thanks to its minimalism, it is capable of powering complex multi-user sites as well as lightweight one-pagers.

## What makes Focus Style unique?
- FS is **minimalistic**: Compared to other CSS frameworks, FS is very lightweight and tries to avoid unnecessary bloat.
- FS is **easy**: It provides clear, consistent naming conventions and helpful utility classes.
- FS is **modern** by default: It embraces new CSS features as soon as they are widely supported and beneficial.
- FS is **responsive** by default: Font sizes and spaces adjust depending on the viewport size.
- FS has a sophisticated **typography system**: Fluid font sizes, mathematical scales and even x-height scales let you optimize the legibility of your texts across all screens… all with a few lines of code.
- FS uses a flexible and well-grown **color system**: Tints, shades and alpha ramps derive from a few anchor colors. You can also choose between solid ramps or alpha ramps.
- FS is **customizable**: Add your own utility classes and remove those you don’t need. Use broad color palettes for complex corporate designs or just a few standalone colors. You’re free to adapt FS to your needs.
- FS makes **testing designs easy**, since it runs on custom properties and can be live edited in your browser’s dev tools.
- FS uses **convention over configuration**, thus some opinionated rules are necessary.

## Which rules apply?
- *No magic numbers!* Please only ever use predefined tokens for consistency and better maintainability.
- *Every component should have zero margin:* Components should be unaware of their outer world. Margins should be handled via one of the parent components, e.g. by using `.fs-flex` with `.fs-gap`. That way, unpredictable margin collapses or double margins in certain situations are prevented. To ensure that, [Block Formatting Context](https://www.smashingmagazine.com/2017/12/understanding-css-layout-block-formatting-context/) should be applied to each component. You can do that by using the `.fs-bfc` utility.
- *Components are unaware of their surroundings:* No dependencies from other objects, the outer world is a black box.
- *Everything is a space:* FS doesn’t distinguish between margins, paddings, heights, widths, etc. Just use `--fs-space--*` for everything. The space scale is limited on purpose to ensure a harmonic layout. It is also linear, so doubling the value means doubling the space. The only exception is `--fs-max-size--*`, since those values are much bigger. Also some token reference `--fs-space--*` for better maintainability, such as `--fs-border-width` and `--fs-border-radius`. The space scale depends on `--fs-font-size-root` and is responsive by default.
- *Float is only used for elements that float:* Self-explanatory, for layout we have better properties nowadays.
- *Naming with double dashes:* A double dash separates a group from its variant (`--fs-border-radius--default`), a single dash is part of a compound name (`--fs-font-size-scale`). T-shirt sizes are abbreviated (`sm`, `md`, `2xl`), all other values are spelled out (`wide`, `large`). Classes are standard BEM. That way, FS reduces confusion and helps with autocomplete.
- *Private properties for internal use only:* You might stumble across files/tokens beginning with an `_` like `--_fs-color--white`. Those are meant for internal reference only and never to be used directly outside their scope in other components or utility classes!

## How does it work?
- *Four layer separation:* Loaded from low to high:
	1. `/src/1-properties/`: the design system.
	2. `/src/2-base-elements/`: minimal HTML reset and element definitions.
	3. `/src/3-utility/`: handpicked helper classes, especially useful for layout and typography. Think twice before introducing a new helper class and increasing code complexity/component dependence.
	4. `/src/4-components/`: some common page elements, optional.
- *Typography scale:* Free your mind of font size values, they’re not needed anymore. Just define the font size root in `--fs-font-size-root.css` (or use the default one) and choose a typography scale in `--fs-font-size-scale.css`. That’s it! Now all font sizes for headlines and such are calculated automatically. In addition: If you want to align different font families visually for advanced typography, you can do so by defining an x-height-scale for each font family in `--fs-font-size-x-height-scale.css`.
- *Color ramps:* Ramps are based on the [universal color palette system](https://uxdesign.cc/the-universal-color-palette-9826deb94f7). The color lightness for `--_fs-color--*--500` should be equal across all color ramps. The ramps only contain the steps actually in use, so that they can be extended later without refactoring, if necessary.
- *Semantic color tokens:* These are the public interface for components and utilities to consume, e.g. `--fs-color--text`. They reference private primitives. Please always use semantic tokens, never literal color values!
- *Private primitives:* They are only used by semantic tokens and should never be consumed directly, e.g. `--_fs-color--*`.

## What’s under the hood?

FS is built with PostCSS and just two plugins:
- `postcss-custom-media` is a polyfill for the upcoming @custom-media standard.
- `postcss-easy-import` resolves glob imports and bundles all layers into one file.

Everything else is native CSS.
