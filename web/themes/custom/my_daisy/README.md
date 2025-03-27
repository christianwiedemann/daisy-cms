# my_daisy

This is a starterkit example to demonstrate how some integrations can be done
like:
- CKEditor 5 stylesheets
- Negative margins in utility classes
- Background gradients

Such configurations/integrations cannot be done in the base theme as
- not enabled in DaisyUI/TailwindCSS default compiled CSS, or
- not impossible to do in a generic way

## Usage

See the
[Starterkit documentation on Drupal.org](https://www.drupal.org/docs/core-modules-and-themes/core-themes/starterkit-theme).

Example command to generate your theme from your `web` folder

```bash
php core/scripts/drupal generate-theme my_daisyui_theme --starterkit my_daisy --path themes/custom
```

## CSS

A default DaisuUI CSS file is provided. To update this file with updates to both the DaisyUI and TaildwindCSS projects

### Using NPM

#### Setup NPM
- copy/rename `package-example.json` to `package.json`
- create empty file `package-json.lock`
  > this encourages NPM packages to be installed in this folder, and not in a folder of a parent NPM project
- install packages `npm update`

#### Build CSS (uses Vite, PostCSS, TailwindCSS)
- `npm run build`
```
❯ npm run build

> build
> NODE_ENV=production  vite build --emptyOutDir

vite v6.2.2 building for production...
transforming (4) ../../components/button/button.pcss.css[vite:css][postcss] Parse error on line 1:
...calc(var(--radius-field) + var(--radius-field) + var(--radius-field)))
------------------------------------------------------------------------^
Expecting end of input, "ADD", "SUB", "MUL", "DIV", got unexpected "RPAREN"

✓ 5 modules transformed.
./components/alert/alert.css            0.09 kB │ gzip:  0.10 kB
./components/accordion/accordion.css    0.13 kB │ gzip:  0.13 kB
./components/button/button.css          0.44 kB │ gzip:  0.23 kB
./dist/css/style.css                  168.54 kB │ gzip: 28.08 kB
✓ built in 1.31s
```

#### Build CSS (uses Vite, PostCSS, TailwindCSS) without mimyifing/compressing CSS
- ```npm run dev``` to build both a CSS file file, wait, and rebuild when a file is updated
```
❯ npm run dev

> dev
> NODE_ENV=development vite build --emptyOutDir

vite v6.2.2 building for production...
✓ 5 modules transformed.
./components/alert/alert.css            0.09 kB │ gzip:  0.10 kB
./components/accordion/accordion.css    0.13 kB │ gzip:  0.13 kB
./components/button/button.css          0.47 kB │ gzip:  0.24 kB
./dist/css/style.css                  178.40 kB │ gzip: 28.60 kB
✓ built in 851ms
```

#### Build CSS (uses Vite, PostCSS, TailwindCSS) and automatically rebuild once a file is updated
- ```npm run watch``` to build both a CSS file file, wait, and rebuild when a file is updated
```
❯ npm run watch

> watch
> NODE_ENV=development vite build --emptyOutDir --watch

vite v6.2.2 building for production...

watching for file changes...

build started...
✓ 5 modules transformed.
./components/alert/alert.css            0.09 kB │ gzip:  0.10 kB
./components/accordion/accordion.css    0.13 kB │ gzip:  0.13 kB
./components/button/button.css          0.47 kB │ gzip:  0.24 kB
./dist/css/style.css                  178.40 kB │ gzip: 28.60 kB
built in 1205ms.

build started...
✓ 1 modules transformed.
./components/alert/alert.css            0.09 kB │ gzip:  0.10 kB
./components/accordion/accordion.css    0.13 kB │ gzip:  0.13 kB
./components/button/button.css          0.47 kB │ gzip:  0.24 kB
./dist/css/style.css                  178.40 kB │ gzip: 28.60 kB
built in 516ms.

build started...
✓ 1 modules transformed.
./components/alert/alert.css            0.09 kB │ gzip:  0.10 kB
./components/accordion/accordion.css    0.13 kB │ gzip:  0.13 kB
./components/button/button.css          0.47 kB │ gzip:  0.24 kB
./dist/css/style.css                  178.40 kB │ gzip: 28.60 kB
built in 468ms.
```

## Update DaisyUI and/or TailwindCSS

- ```npm update```
- ```npm run build```

### Clear cache
- ```drush cache:rebuild```

## Add TailwindCSS Typography support

### Add the ```@tailwindcss/typography```
- ```npm install @tailwindcss/typography```

### Add TailwindCSS Typography to the project

#### Edit ```src/css/input.css```
- Add ```@plugin "@tailwindcss/typography";``` to ```src/css/input.css```

```css
/**
 * Import TailwindCSS Typography
 * - Should be placed **before** plugging in DaisyUI
 */
@plugin "@tailwindcss/typography";

/**
 * Import DaisyUI excluding DaisyUI reset.css as Tailwind already provide same mechanism (Preflight).
 * We exclude DaisyUI reset.css as it prevents style from base layer to be applied.
 */
@plugin "daisyui"{
    exclude: reset;
}
```

## Add TailwindCSS Forms support

### Add the ```@tailwindcss/forms```
- ```npm install @tailwindcss/forms```

### Add TailwindCSS Typography to the project

#### Edit ```src/css/input.css```
- Add ```@plugin "@tailwindcss/forms";``` to ```src/css/input.css```

```css
/**
 * Import TailwindCSS Typography
 * - Should be placed **before** plugging in DaisyUI
 */
@plugin "@tailwindcss/typography";

/**
 * Import TailwindCSS Forms
 * - Should be placed **before** plugging in DaisyUI
 */
@plugin "@tailwindcss/forms";

/**
 * Import DaisyUI excluding DaisyUI reset.css as Tailwind already provide same mechanism (Preflight).
 * We exclude DaisyUI reset.css as it prevents style from base layer to be applied.
 */
@plugin "daisyui"{
    exclude: reset;
}
```

### Update CSS
- `npm run build`

### Clear cache
- `drush cache:rebuild`
