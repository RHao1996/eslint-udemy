# Match Their Paths

`angular-module-names/match-their-paths` rule requires your `angular.module` name to match the path of the file the 
module is in relative to some specified root.

There's another rule, [`angular/file-name`](https://github.com/Gillespie59/eslint-plugin-angular/blob/master/docs/rules/file-name.md), 
which can be used to ensure that the `angular.module` name follows some established pattern. However, that rule doesn't 
pay any attention to the name of the file the module is in. Hence, it permits files and modules to be named radically 
different things.

## Rule Details

This rule takes no arguments.

The following patterns are considered warnings:

```js 

// in some-path/that-has/some-nice.ng-directive.js

angular.module('some-random/module-name', () => {});

```

The following patterns are not considered warnings:

```js

// in some-path/that-has/some-nice.ng-directive.js

angular.module('some-path/that-has/some-nice.ng-directive', () => {});
 
```
