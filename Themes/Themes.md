# Themes


Dynamic Includes

```
:root {
	/* @themeset(theme.colors.accent.{A}, '--theme-accent-{A}', 'color-csv-rgb') */
	/* @themeset(theme.colors.gray.{A}, '--theme-gray-{A}', 'color-csv-rgb') */

	/* use @themeset() to automatically create rules based on a pattern. */
	
	/* @themeset(theme.colors.mono.{A}, '--theme-{A}', 'color-csv-rgb') */
	
	/* creates:
		--theme-white: 255, 255, 255;
		--theme-black: 0, 0, 0;
	*/
	
	/* or use theme() to just get a single theme value.
	--theme-white: /* @theme(theme.colors.mono.white, 'color-csv-rgb') */;
	--theme-black: /* @theme(theme.colors.mono.black, 'color-csv-rgb') */;

	/* Creates the same thing:
		--theme-white: 255, 255, 255
		--theme-black: 0, 0, 0
	*/
	
}
```

```YAML
layout:
	colors:
		mono:
			white: color
			black: color
		accent:
			50: color
			100: color
			200: color
			300: color
			400: color
			500: color
			600: color
			700: color
			800: color
			900: color
		gray:
			50: color
			100: color
			200: color
			300: color
			400: color
			500: color
			600: color
			700: color
			800: color
			900: color

values:
	colors:
		mono:
			white: #ffffff
			black: #000000
		...

```
