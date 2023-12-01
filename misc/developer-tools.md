# Developer Tools

## User Code Snippets in VSCode

* Writing shortcuts for commonly used functions
* Click "Settings" at bottom left -> "User Snippets" -> "Global File" -> Add Code snippets

```snippets
	"Print to console": {
		"scope": "javascript,typescript",
		"prefix": "cl",
		"body": [
			"console.log();"
		],
		"description": "Log output to console"
	}
```



## Live Server

* For more convenient development process, no more need to refresh the browser with each code update.

#### Installation

1. User VSCode extension: live-server
   1. Click "Go Live" at the bottom right of IDE
2. Node.js

```
npm install live-server -g
```

3. Or simply reload browser (lol)
