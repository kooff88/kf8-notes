# semver

[semver](https://www.npmjs.com.cn/misc/semver/) 是一个版本控制的node的插件. 

简单用法总结:  

```
	semver.valid('1.2.3') // true
	semver.valid('a.b.c') // false
	semver.clean('  =v1.2.3  ') // '1.2.3'
	semver.satisfies('1.2.3', '1.x || >=2.5.0' || 5.0.0 - 7.2.3) // true
	semver.gt('1.2.3', '9.8.7') // false
	semver.lt('1.2.3', '9.8.7') // true

```


通过以下代码可以用来管理node,和npm 的版本的控制  

```js
	var chalk = require('chalk');
	var semver = require('semver');
	var packageConfig = require('../package.json');
	var shell= require('shelljs');
	function exec (cmd) {
		return require('child_process').execSync(cmd).toString().trim()
	}

	var versionRequirements = [
		{
			name: 'node',
			currentVersion: semver.clean(process.version),
			versionRequirement: packageConfig.engines.node
		},

	]

	if (shell.which('npm')) {
		versionRequirements.push({
			name: 'npm',
			currentVersion: exec('npm --version'),
			versionRequirement: packageConfig.engines.npm
		})
	}


	module.exports = function () {
		var warnings = []
		for (var i = 0; i< versionRequirements.length; i++){
			var mod = versionRequirements[i]
			if (!semver.satisfies(mod.currentVersion, mod.versionRequirement)) {
				warnings.push(mod.name + ': ' +
		        chalk.red(mod.currentVersion) + ' should be ' +
		        chalk.green(mod.versionRequirement)
			}
		}

		if (warnings.length) {
			console.log('')
			console.log(chalk.yellow('To use this template, you must update following to modules:'))
			console.log()

			for (var i = 0; i < warnings.length; i++) {
			  var warning = warnings[i]
			  console.log('  ' + warning)
			}
			console.log()
			process.exit(1)
		}

	}

```






