Udemy ESLint Packages
=====================

This repository has [*ESLint*](https://www.github.com/eslint/eslint) related packages used by various Udemy projects. 
It is owned by [@udemy/team-f](https://github.com/orgs/udemy/teams/team-f), but everyone is welcome to contribute.
Please refer to the [Contributing](#contributing) section to learn more.

This repository uses [*Lerna*](https://github.com/lerna/lerna) to manage multiple [*npm*](https://www.npmjs.com/) packages. We 
configured Lerna to use [*Yarn Workspaces*](https://yarnpkg.com/lang/en/docs/workspaces/) under the hood.

# Installation

Refer to each package's *Installation* section in order to learn how to install each package.
There is no top-level installation. Though, [`eslint-config-udemy-basics`](packages/eslint-config-udemy-basics)
and [`eslint-plugin-udemy`](packages/eslint-plugin-udemy) are good starting points.

# Commands

In order to contribute to this repository, you need to have a basic understanding of 
[Lerna commands](https://github.com/lerna/lerna#commands). In a nutshell, 
there are three important commands to know:

* **[`lerna add`](https://github.com/lerna/lerna#add):** In order to add a new dependency to an existing package's 
`package.json` file, you'd run `` `yarn bin`/lerna add dependency-name --scope=package-name``. E.g.:
    
    ```
    $ `yarn bin`/lerna add eslint-plugin-lodash --scope=eslint-config-udemy-website
    ``` 
    
* **[`lerna bootstrap`](https://github.com/lerna/lerna#bootstrap):** In order to install all of the dependencies
for every package, you can simply run `` `yarn bin`/lerna bootstrap``.
* **[`lerna publish`](https://github.com/lerna/lerna#publish):** In order to publish your changes to npm, you
can simply run `` `yarn bin`/lerna publish ``. It will prompt you for a version number for each package you have 
changed.

# List of available packages

We individually publish all folders inside [`packages`](packages) as a separate npm package. These packages are
owned by our [Udemy npm organization](https://www.npmjs.com/org/udemy).

* **[`eslint-config-udemy-basics`](packages/eslint-config-udemy-basics):** A basic ESLint configuration for writing 
ES2015 JavaScript code. This is used by various Udemy projects.
* **[`eslint-config-udemy-babel-addons`](packages/eslint-config-udemy-babel-addons):** 
[*Babel*](https://github.com/babel/babel) specific ESLint configuration. Extended by 
[`eslint-config-udemy-website`](packages/eslint-config-udemy-website).
* **[`eslint-config-udemy-jasmine-addons`](packages/eslint-config-udemy-jasmine-addons):** 
[*Jasmine*](https://github.com/jasmine/jasmine) specific ESLint configuration. Extended by 
[`eslint-config-udemy-website`](packages/eslint-config-udemy-website).
* **[`eslint-config-udemy-react-addons`](packages/eslint-config-udemy-react-addons):**
[*React*](https://github.com/facebook/react) specific ESLint configuration. Extended by 
[`eslint-config-udemy-website`](packages/eslint-config-udemy-website).
* **[`eslint-config-udemy-website`](packages/eslint-config-udemy-website):**
The ESLint configuration used by 
[`udemy/website-django/static/`](https://github.com/udemy/website-django/tree/master/static/.eslintrc.js) codebase.
* **[`eslint-plugin-udemy`](packages/eslint-plugin-udemy):**
A set of custom ESLint rules written for Udemy, by Udemy. These rules are mainly used by  
[`eslint-config-udemy-website`](packages/eslint-config-udemy-website).

# Contributing

Install [*Yarn v1.3.2*](https://github.com/yarnpkg/yarn/releases/tag/v1.3.2) globally. 

    $ npm install -g yarn@1.3.2

Install all dependencies locally.

    $ yarn install
    $ `yarn bin`/lerna bootstrap
    
Run tests to verify everything is working.

    $ yarn run test

## Updating an existing package

1. Create a new branch.
1. Add any new dependencies to any of the packages via `lerna add`.
1. Install all dependencies (see above).
1. Make your necessary source file changes.
1. Write your tests if applicable.
1. Do *NOT* update version numbers in `package.json` files (`lerna publish` does it for you).
1. Run `yarn run test` to make sure all tests pass.
1. Commit/push your changes.
1. Create a pull request against master.
1. Once your pull request is approved, run `lerna publish` in order to publish your changes to npm.
   - Ideally we would first merge the pull request to master, then publish master to npm, but `lerna publish`
     creates a "Publish" commit which would have to be pushed to master, and non-admins cannot push
     directly to master.
   - If this is your first time running `lerna publish`, you will be prompted to first run
     `npm adduser`. If you don't have an npm account, create one at <https://www.npmjs.com/signup>,
     and ping [@udemy/team-f](https://github.com/orgs/udemy/teams/team-f) to add your account to
     the [Udemy npm organization](https://www.npmjs.com/org/udemy).
   - If `lerna publish` doesn't pick up your changes (this happens if you had to run `npm adduser`),
     you can manually publish a package via e.g. `cd packages/eslint-config-udemy-website; npm publish`.
1. Confirm your changes were published to npm by checking the npm website,
   e.g. <https://www.npmjs.com/package/eslint-config-udemy-website>.
1. `lerna publish` should have created a "Publish" commit, which includes changes to CHANGELOG.md and package.json.
   See [#4a7ba34](https://github.com/udemy/eslint-udemy/commit/4a7ba340cee2bbbabe37b88efe5404a820bc1316) for example.
   Push this commit. Merge your pull request.
1. Go to the repository where you'd use these new ESLint rule changes.
1. Update the `package.json` dependencies to any `eslint-config|plugin-udemy-*` package as necessary.
1. Run `yarn install` to install the changes and to be able to start using the package.

You can always reach out to [@udemy/team-f](https://github.com/orgs/udemy/teams/team-f) on the 
[#dev-team-f Slack channel](https://udemy.slack.com/messages/dev-team-f).
 
## Adding a new package

1. Get in touch with [@udemy/team-f](https://github.com/orgs/udemy/teams/team-f) on the 
[#dev-team-f Slack channel](https://udemy.slack.com/messages/dev-team-f) to assess the need for a
new npm package to avoid any duplicate work.
1. Once there is consensus, create a new folder under [packages](packages/) folder under the
desired npm package name.
1. Use `index.js` as the package's main entry point, and `tests.js` as its entry point for tests.
1. Make sure `package.json` has the necessary information, per existing examples.
1. Make sure the new package has a meaningful `README.md` and a valid `LICENSE` file.
1. Follow the regular pull request and `lerna publish` flow as described above.

## Writing commit messages

We use [Conventional Commits](https://conventionalcommits.org) for commit guidelines. The commit message should be 
structured as follows: 



```
<type>[optional scope]: <description>

[optional body]

[optional footer]
```

_Example_

```
feat: Introduce eslint-config-tester

It is a utility library to write tests for ESLint configurations.
```

The commit message format is 
important because these messages are used to create a changelog for each release.
