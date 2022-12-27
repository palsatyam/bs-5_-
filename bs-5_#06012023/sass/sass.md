```Sass
Utilize our source Sass files to take advantage of variables, maps, mixins, and functions to help you build faster and customize your project.


```File structure

your-project/
├── scss
│   └── custom.scss
└── node_modules/
    └── bootstrap
        ├── js
        └── scss

```Importing

// Custom.scss
// Option A: Include all of Bootstrap

// Include any default variable overrides here (though functions won't be available)

@import "../node_modules/bootstrap/scss/bootstrap";

// Then add additional custom code here
Copy
// Custom.scss
// Option B: Include parts of Bootstrap

// 1. Include functions first (so you can manipulate colors, SVGs, calc, etc)
@import "../node_modules/bootstrap/scss/functions";

// 2. Include any default variable overrides here

// 3. Include remainder of required Bootstrap stylesheets
@import "../node_modules/bootstrap/scss/variables";
@import "../node_modules/bootstrap/scss/mixins";

// 4. Include any optional Bootstrap components as you like
@import "../node_modules/bootstrap/scss/root";
@import "../node_modules/bootstrap/scss/reboot";
@import "../node_modules/bootstrap/scss/type";
@import "../node_modules/bootstrap/scss/images";
@import "../node_modules/bootstrap/scss/containers";
@import "../node_modules/bootstrap/scss/grid";


    ```Variable defaults


    // Required
@import "../node_modules/bootstrap/scss/functions";

// Default variable overrides
$body-bg: #000;
$body-color: #111;

// Required
@import "../node_modules/bootstrap/scss/variables";
@import "../node_modules/bootstrap/scss/mixins";

// Optional Bootstrap components here
@import "../node_modules/bootstrap/scss/root";
@import "../node_modules/bootstrap/scss/reboot";
@import "../node_modules/bootstrap/scss/type";
// etc


```Maps and loops
Bootstrap includes a handful of Sass maps, key value pairs that make it easier to generate families of related CSS. We use Sass maps for our colors, grid breakpoints, and more. Just like Sass variables, all Sass maps include the !default flag and can be overridden and extended.

```Modify mapAll variables in the $theme-colors map are defined as standalone variables. To modify an existing color in our $theme-colors map, add the following to your custom Sass file:

Example:--
$primary: #0074d9;
$danger: #ff4136;

Later on, these variables are set in Bootstrap’s $theme-colors map:

Copy
$theme-colors: (
  "primary": $primary,
  "danger": $danger
);

```Add to map
Add new colors to $theme-colors, or any other map, by creating a new Sass map with your custom values and merging it with the original map. In this case, we’ll create a new $custom-colors map and merge it with $theme-colors.
// Create your own map
$custom-colors: (
  "custom-color": #900
);

// Merge the maps
$theme-colors: map-merge($theme-colors, $custom-colors);


```Remove from mapTo remove colors from $theme-colors, or any other map, use map-remove. Be aware you must insert it between our requirements and options:

Copy
// Required
@import "../node_modules/bootstrap/scss/functions";
@import "../node_modules/bootstrap/scss/variables";
@import "../node_modules/bootstrap/scss/mixins";

$theme-colors: map-remove($theme-colors, "info", "light", "dark");

// Optional
@import "../node_modules/bootstrap/scss/root";
@import "../node_modules/bootstrap/scss/reboot";
@import "../node_modules/bootstrap/scss/type";
// etc

```Required keys
Bootstrap assumes the presence of some specific keys within Sass maps as we used and extend these ourselves. As you customize the included maps, you may encounter errors where a specific Sass map’s key is being used.

For example, we use the primary, success, and danger keys from $theme-colors for links, buttons, and form states. Replacing the values of these keys should present no issues, but removing them may cause Sass compilation issues. In these instances, you’ll need to modify the Sass code that makes use of those values.

```Functions
Colors
Next to the Sass maps we have, theme colors can also be used as standalone variables, like $primary.

Copy
.custom-element {
  color: $gray-100;
  background-color: $dark;
}


```Color contrast

In order to meet WCAG 2.0 accessibility standards for color contrast, authors must provide a contrast ratio of at least 4.5:1, with very few exceptions.

An additional function we include in Bootstrap is the color contrast function, color-contrast. It utilizes the WCAG 2.0 algorithm for calculating contrast thresholds based on relative luminance in a sRGB colorspace to automatically return a light (#fff), dark (#212529) or black (#000) contrast color based on the specified base color. This function is especially useful for mixins or loops where you’re generating multiple classes.

For example, to generate color swatches from our $theme-colors map:

Copy
@each $color, $value in $theme-colors {
  .swatch-#{$color} {
    color: color-contrast($value);
  }
}