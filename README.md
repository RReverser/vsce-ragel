# Ragel syntax support for Visual Studio Code

This extension provides syntax highlighting & snippets support for Ragel State Machine Compiler syntax.

You can read more about Ragel here: http://www.colm.net/open-source/ragel/

If you want to show Ragel errors in Visual Studio Code on compile, add the following snippet to your `.vscode/tasks.json`:

```javascript
{
	"version": "0.1.0",

	// The command is ragel. Assumes that ragel has been installed globally
	"command": "ragel",

	// The command is a shell script
	"isShellCommand": true,

	// Show the output window only if unrecognized errors occur.
	"showOutput": "silent",

	// args is the HelloWorld program to compile.
	"args": ["--error-format=msvc", "HelloWorld.rl"],

	// use custom ragel problem matcher to find compile problems
	// in the output.
	"problemMatcher": {
		// The problem is owned by the typescript language service. Ensure that the problems
		// are merged with problems produced by Visual Studio's language service.
		"owner": "ragel",
		// The file name for reported problems is relative to the current working directory.
		"fileLocation": ["relative", "${cwd}"],
		// The actual pattern to match problems in the output.
		"pattern": {
			// The regular expression. Matches HelloWorld.rl(2,10): graph lookup of "Something" failed
			"regexp": "^([^:]+)\\((\\d+,\\d+)\\):\\s+(.*)$",
			// The match group that denotes the file containing the problem.
			"file": 1,
			// The match group that denotes the problem location.
			"location": 2,
			// The match group that denotes the problem's message.
			"message": 3
		}
	}
}
```

And you will get error reporting like in the screenshot below:

![](https://cloud.githubusercontent.com/assets/557590/13816130/1249da8a-eb85-11e5-958d-2099c7283f85.png)
