# What's the point of a linter?

One of the things developers love and hate most about JavaScript is the fact that it is a dynamic, loosely-typed language. You want to turn that string into an integer? No problem. This object needs to be an array? It can do that, too.

But because JavaScript is so flexible (and lacks a compilation process), it is also especially prone to developer errors, and we typically find those errors only through code execution. And that's where [linters](<https://en.wikipedia.org/wiki/Lint_(software)>) come in.

Linters statically analyze your code to quickly find problems. They can suggest fixes or even fix code automatically sometimes, and linting tools like ESLint allow developers to discover problems with their JavaScript code without executing it.

The bottom line is: linters help make us better developers by alerting us to anti-patterns and bugs _before_ we run our code. And ESLint is the best linter available today.

**In this lesson, we'll learn how to add it to our project and set it up to run all the time in our code editor during development.**

> Fun fact: Create React Apps already comes with some more generic ESLint configurations set under the hood, but we're going to take it up a notch and learn how to configure it to our specific project needs.

### What is ESLint?

[ESLint](https://eslint.org/) is the currently preferred linter for JavaScript projects of all sorts. It's been around since 2013, and its primary reason for being is to allow developers to create their own preferred set of linting rules.

ESLint is designed so that all the rules work independently of each other, and they can be added and removed or turned on and off at will. It's very plug-and-play. Each project use case is unique in some ways, and ESLint knows and embraces this, making itself easy to configure to meet the needs of the project.

In addition to being highly configurable, allowing you to add any and all the rules you desire (of which [there are many](https://eslint.org/docs/rules/)), ESLint also integrates very well with lots of code editors, VSCode included. Put a pin in that statement for later in the lesson.

#### Airbnb: The ESLint config of choice for React

Some might argue that ESLint is _so_ unopinionated that it's not very useful starting from scratch. And I'm inclined to agree; there's a lot of rules to look through and decide which ones are the standards your team wants to adhere to.

A fairly common practice that's sprung up today is that projects will use an already-defined ESLint config as a starting point and then make tweaks to the originally defined set of rules laid out to suit the team's needs and style of development.

One such config that's gained a large and loyal following, especially amongst React development teams, is the [ESLint config set forth by the Airbnb team](https://airbnb.io/javascript/react/).

It's a robust style guide based on standards that are currently prevalent in JavaScript, and as the team docs themselves put it, the config serves as a "mostly reasonable approach to React and JSX".

Each rule is clearly laid out in the [documentation](https://airbnb.io/javascript/react/) with code examples, and some even have extra explanations, depending on the rule. I highly recommend giving it a read; a lot of the rules indirectly spell out React best practices that any codebase can benefit from. But that's enough talk about Airbnb's ESLint config. Let's start adding it to our project.

### Remove any pre-existing ESLint config files your project may have

It's worth pointing out that if you're developing on an already existing React app, it may already have an ESLint file in it. This file could be something like `.eslintrc.yaml`, `.eslintrc.json`, `.eslintrc.js`. (These are all valid ESLint configs — it's flexible in what it will accept like Prettier.)

I would strongly recommend you delete it completely and start fresh. ESLint's made many improvements since that file was probably set up, and rules that may previously have been needed are now default, configs that existed may have been renamed, etc. Instead of trying to merge the existing ESLint file with the new one I detail below, I'd start over.

> Besides, if you realize there are some rules you can't live without, your version control system will remember the old config file, and you can grab whatever you need from it.

### Download all the required ESLint npm packages

Unlike setting up Prettier, in our previous lesson, which required just one new npm package, ESLint requires _a bunch_.

If you read the [ESLint npm documentation](https://www.npmjs.com/package/eslint-config-airbnb), it outlines all the peer dependencies (peer deps) that the Airbnb ESLint depends on, but instead of just installing whatever the latest version is of each peer dep, it provides a quick shell script to identify the correct version for each additional dependency for the current version of the Airbnb ESLint library.

So, open up the code in your IDE and `cd` into the `root` folder from the terminal, and run the following commands:

```shell
npm info "eslint-config-airbnb@latest" peerDependencies
```

Once you run this, you should see all the required peer deps for whatever version of the `eslint-config-airbnb` npm package. It will look something like this in your terminal.

Now, if you have a version of npm installed that's `npm` v5 or above, there's a little shortcut you can take to install all these dependencies so that you don't have to do them one by one.

After checking your `npm` version in the terminal with `npm -v` and confirming it's over version 5, paste this command into the terminal:

```shell
npx install-peerdeps --dev eslint-config-airbnb
```

> Why yes, that command says `npx`, and yes, we're using `yarn` in our project as our package manager.
>
> NPX is smart enough that it can detect we're using Yarn as our package manager and act accordingly.
>
> If you're not as familiar, `npx` is a tool intended to help round out the experience of using packages from the npm registry — the same way npm makes it super easy to install and manage dependencies hosted on the registry, NPX makes it easy to use CLI tools and other executables hosted on the registry.
>
> Basically, `npx` makes it possible to install `devDependencies` to projects locally without having to install them globally.
>
> It's also great if you just want to try a CLI tool once without having to install it globally. Just use `npx <command>` when `<command>` isn’t already in your $PATH, and `npx` will automatically install a package with that name from the npm registry for you and invoke it.
>
> If you'd like to learn more about `npx`, this [article is full of useful info](https://blog.npmjs.org/post/162869356040/introducing-npx-an-npm-package-runner.html#:~:text=npx%20is%20a%20tool%20intended,executables%20hosted%20on%20the%20registry.).

But we're not quite done yet. We've got a few more dependencies we need to install for ESLint to work properly with this Create React App application.

Here are the other dependencies you need to install. These are so Prettier and the latest version of Create React App will play nice with all of our ESLint rules.
```shell
yarn add -D eslint @babel/eslint-parser eslint-config-prettier @babel/core eslint-plugin-prettier eslint-plugin-react
```

### Create .eslintrc file with the following code

```json
{
  "extends": [
    "airbnb",
    "airbnb/hooks",
    "eslint:recommended",
    "prettier",
    "plugin:jsx-a11y/recommended"
  ],
  "parser": "@babel/eslint-parser",
  "parserOptions": {
    "babelOptions": {
      "presets": ["@babel/preset-react"]
    },
    "ecmaVersion": 8,
    "requireConfigFile": false
  },
  "env": {
    "browser": true,
    "node": true,
    "es6": true,
    "jest": true
  },
  "rules": {
    "react/react-in-jsx-scope": 0,
    "react-hooks/rules-of-hooks": "error",
    "no-console": 0,
    "react/state-in-constructor": 0,
    "indent": 0,
    "linebreak-style": 0,
    "react/prop-types": 0,
    "jsx-a11y/click-events-have-key-events": 0,
    "react/jsx-filename-extension": [
      1,
      {
        "extensions": [".js", ".jsx"]
      }
    ]
  },
  "plugins": ["prettier", "react", "react-hooks"]
}
```
