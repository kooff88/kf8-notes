# fs-extra

提供比Node中FS模块更多的方法，当然FS中的模块可继续使用。    


- [fs-extra在github](https://github.com/jprichardson/node-fs-extra)  


## Example

```js
	const fs = require('fs-extra')

	// Async with promises

	fs.copy('/tmp/myfile', 'tmp/mynewfile')
		.then(() => console.log('success!'))
		.catch(err => console.error(err))

	// Async with callbacks
	fs.copy('/tmp/myfile', '/tmp/mynewfile', err => {
		if (err) return console.error(err)
		console.log('success!')
	})


	// Sync
	try{
		fs.copySync('tmp/myfile', 'tmp/mynewfile')
		console.log('success!')
	} catch (err){
		console.log(err)
	}

	// Async/Await

	async function conpFiles () {
		try {
			await fs.copy('/tmp/myfile', 'tmp/mynewfile')
			console.log('success!')
		} catch (err) {
			console.log(err)
		}
	}

	copyFiles()

```
