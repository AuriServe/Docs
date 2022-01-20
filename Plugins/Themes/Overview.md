# Overview
Catalogs and loads themes for use in rendered HTML, such as in the Pages plugin.

## Directives
The following directives are supported by the themes Plugin by writing them within a comment in your source files. Some directives require a specific language, which is noted below.

### @color-swatch(optionPath, propertyPrefix, format)
(CSS)

Replaces the comment with property declarations for each color in a Color Swatch option. For example:

**`manifest.yaml`**
```yaml
options:
- key: color.primary
	label: Primary Color
	type: color_swatch
	swatches:
		burgundy:
			50: '#FFE3E3'
			100: '#FFBDBD'
			200: '#FF9B9B'
			300: '#F86A6A'
			400: '#EF4E4E'
			500: '#dc2e2e'
			600: '#ca1e24'
			700: '#ad1a20'
			800: '#8A041A'
			900: '#610316'

presets:
	refined:
		default: true
		values:
			color.primary: burgundy
```

**style.css**
```css
#page {
	/*@color-swatch(color.primary, --color-primary, rgb)*/
}
```

**Resolves to:**
```css
#page {
	--color-primary-50: 255,227,227;
	--color-primary-100: 255,189,189;
	--color-primary-200: 255,155,155;
	--color-primary-300: 248,106,106;
	--color-primary-400: 239,78,78;
	--color-primary-500: 220,46,46;
	--color-primary-600: 202,30,36;
	--color-primary-700: 173,26,32;
	--color-primary-800: 138,4,26;
	--color-primary-900: 97,3,22;
}
```

### @theme(optionPath, format?)
(CSS)

Replaces the comment with the property at the specified path, optionally formatting it with the format provided.

### @if(condition), @elseif(condition), @else, @endif
(HTML, CSS)

Used in tandem to represent a conditional expression. For example:

**`manifest.yaml`**
```yaml
options:
- key: option.dark
	type: boolean

presets:
	light:
		default: true
		values:
			option.dark: false
	dark:
		values:
			option.dark: true
```

**style.css**
```css
#page {
	/*@if(option.dark)*/
	color: white;
	background-color: black;
	/*@else*/
	color: black;
	background-color: white;
	/*@endif*/
}
```

**Resolves to:**
```css
#page {
	color: black;
	background-color: white;
}
```

All conditional expressions must end with an `@endif` directive, and currently, nested conditionals are not supported.