# Pixim-animate-container

"Pixim-animate-container" is a plugin for using content published by Adobe Animate with "[Pixim.js](https://github.com/tawaship/Pixim.js)".

[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)

---

## Support version

- A complete set of content published with Adobe Animate version 20.02
- pixi.js 5.3.2
- Pixim.js 1.6.1

I have not confirmed the operation on other versions.

## How to use

1. Install

```sh
git clone https://github.com/tawaship/Pixim-animate-container
```

<br>

```html
<script src="https://code.createjs.com/1.0.0/createjs.min.js"></script>
<script src="/path/to/lib/pixi.5.3.2.min.js"></script>
<script src="/path/to/lib/Pixim.min.js"></script>
<script src="/path/to/dist/Pixim-animate-container.min.js"></script>
<script src="[your content]"></script>
```

2. Use

```javascript
Pixim.animate.prepareAsync(
	"[conposition id]", // "lib.properties.id" in Animate content.
	"[content directory path]", // Directory path of Animate content.
	{
		useSynchedTimeline: true
	}
.then(function(lib) {
	const app = new Pixim.Application();
	
	const Game = Pixim.Content.create();
	
	Game.setConfig({
		width: 450,
		height: 800
	});
	
	Game.defineLibraries({
		root: class Root extends PIXI.Container {
			constructor($) {
				super();
				
				const container = this.addChild(new Pixim.animate.Container());
				
				const cls = $.vars.lib.game; // The class you want to use.
				container.addCreatejs(new cls());
			}
		}
	});
	
	const game = new Game();
	game.addVars({
		lib: lib
	});
	
	app
		.fullScreen()
		.attachAsync(game)
		.then(function() {
			app.play();
		});
});
```

## Overrides

- createjs.MovieClip = [CreatejsMovieClip](https://tawaship.github.io/Pixim-animate-container/docs/pixim/classes/createjsmovieclip.html)

## Samples

[github](https://tawaship.github.io/Pixim-animate-container/samples/)