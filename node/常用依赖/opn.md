# opn

打开浏览器的依赖

## 使用方法

```
	const opn = require('opn');

	// opens the image in the default image viewer

	opn('unicorn.png').then(() => {
		// image viewer closed
	});

	// opens the url in the default brower
	opn('http://sindresorhus.com');

	// sepecify the app to open in
	opn('http://sindresorhus.com', {app:'firefox'});

	// specify app arguments
	opn('http://sindresorhus.com', { app:[ 'google chrome', '--incognito' ] })

```
