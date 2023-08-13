# Amatis Food delivery

Amatis food delivery is a web-based application that allows users to order food from various restaurants and get it delivered to their doorstep. The frontend of the application is built using React, a popular JavaScript library for building user interfaces, and Tailwind CSS, a utility-first CSS framework for styling web applications. With Amatis food delivery, users can browse restaurants, view menus and prices, add items to their cart, apply discounts, and complete their orders online. The application also includes a user management system that allows users to create accounts, save their delivery addresses, and view their order history. Overall, Amatis food delivery is a great solution for anyone who wants to enjoy delicious food from the comfort of their own home.

## Table of Contents

- [Description](#description)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Description

Amatis food delivery is a sample project designed for frontend developers who are looking to learn about build automation, containerization, and server setup. The project is built using React, a popular JavaScript library for building user interfaces, and Tailwind CSS, a utility-first CSS framework for styling web applications. In addition to these technologies, the project includes a number of other tools and technologies that are commonly used in modern web development.

One of the key features of the project is its use of Docker for containerization. This allows developers to easily build and deploy the application in a consistent way, regardless of the environment in which it is being run. The project also includes Docker Compose, which is used to configure and manage the various containers that make up the application.

In addition to containerization, the project also includes Github Actions for build automation. This allows developers to automatically build and test the application whenever changes are pushed to the source code repository. The application also includes ESLint for code linting, which helps to ensure that the code adheres to best practices and coding standards.

Finally, the project includes Nginx for server setup. Nginx is a powerful web server that is commonly used in production environments, and can be used to serve static files, reverse proxy to application servers, and handle SSL termination. By including Nginx in the project, developers can gain experience in configuring and managing a production-grade web server.

Overall, Amatis food delivery is an excellent project for frontend developers who are looking to gain experience in containerization, build automation, code linting, and server setup.

## Installation

### 1. Install dependencies

```
yarn install
```

### 2. Run Applications

```
yarn dev
```

If you run project and get error, make sure you've installed `Node.js >= 16` and `yarn`.

You can run `cat package.json` to see available commands.

## Environment

### `✅` VS Code editor highly recommended

### Recommended plugins

- `✅` [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- `✅` [Prettier ESLint](https://marketplace.visualstudio.com/items?itemName=rvest.vs-code-prettier-eslint)
- `✅` [Code Spell Checker Plugin](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)
- `✅` [Auto Import](https://marketplace.visualstudio.com/items?itemName=steoates.autoimport)
- `✅` [IntelliCode](https://marketplace.visualstudio.com/items?itemName=VisualStudioExptTeam.vscodeintellicode)
- `✅` [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)
- `✅` [JavaScript (ES6) code snippets](https://marketplace.visualstudio.com/items?itemName=xabikos.JavaScriptSnippets)
- `✅` [GitLens — Git supercharge](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)

## General Structure

```
public
  |-- assets
      |-- fonts
          Web fonts.
      |-- icons
          SVG icons, and anything that looks like an icon.
      |-- images
          Static images, like backgrounds.
      `-- logo
          Various versions of logotype and basic branding.
  |-- data
      Static `json` files that can be called from the API,
      allowing them to be requested on demand and hence avoid bundling them into project.
  `-- manifest
      PWA related images.
src
  |-- components
      Contains reusable components, such as: Navigation, Menus, etc...
      These components usually contain project specific data or behavior, they
      could make API calls and perform complex logic.
  |-- libraries
      Libraries are non-react units of code, used throughout project.
      The best example of this is fetch.
  |-- pages
      Pages are components that connects to routes, and render final view
      that user interacts with. They're usually named the same as actual route (ie URL path).
  |-- services
      Services are used to abstract API calls, and define request and response data types.
```

Most of folders contains `index.jsx` file, which will export all files, and allow easy and readable inclusion in style of
`import { AuthAPI, logger } from '@app/services'`.

### Do's and don'ts

- `✅` DO: Follow consistent naming of files (capitalization, CamelCase, easy to understand names).
- `🔴` DON'T: Created new components if used only in one place (on one screen).
- `🔴` DON'T: Needlessly create deeply nested folders.
- `🔴` DON'T: Introduce big data chunks inside the actual code. Store them in `/public/data/` and request them with API when needed.
- `🔴` DON'T: Add anything in the root (`src`) part of the project.
- `🔴` DON'T: Non-component separations - global files (i.e. global constants, types, styles).
- `🔴` DON'T: Introduce needles, heavy - in scope, size or complexity, external dependencies.

## Environment

- `🔴` DON'T, `🔴` DON'T: change `environment.jsx` unless you're introducing a new variable,
- `✅` DO: change `environment.dev.jsx` and set your own values.
- `✅` DO: if you're introducing a new variable to `environment.jsx`, use descriptive and easy to understand naming
- `✅` DO: Include `environment` in following way: `import env from '@app/environment'`
- `🔴` DON'T: import dev environment `import env from '@app/environment.dev'`!

## Code Style

We're following simple rules as defined in `.eslint.json`:

- `✅` DO: 2 spaces, no tabs
- `✅` DO: single quite for JS, double quite fro HTML/Element Props
- `✅` DO: no semicolons
- `✅` DO: keep lines short
- `🔴` DON'T: leave unused variable (build will fail!)
- `🔴` DON'T: leave console.log or console.error in code

We're using TypeScript:

- `✅` DO: define proper and up-to-date types (especially for API request/response)
- `✅` DO: generally: keep types in file with code; libraries/services: types can be stored in external file, named: `myFile.d.jsx` (note the .d);
- `🔴` DON'T: use `any` notation (build will fail)
- `🔴` DON'T: create common repository of types (i.e. `src/types` directory)

## React Component Structure

Components are structured in a following way:

```JSX
// Interfaces stays with component, and is usually not exported.
interface MyComponentProps {}
// Chunks of static data (especially texts that are to change often) can stay
// outside of components. This makes them easy to access and benefits
// performance. No need to `useRef` if something is not about to change
// from within component.
const COMPONENT_SPECIFIC_CONST = null

const MyComponent: React.FC<MyComponentProps> = props => {

  // useEffect and other use* functions are always placed on top
  useEffect(() => {}, [])

  // Event function (like onClick, onChange) are
  // preferable prexied with `handle`
  function handleClick() {}

  // API calls are preferable prefixed with fetch
  function fetchUsers() {}

  // Functions that will return React element are prefixed with `render`
  // and are placed above return
  function renderSection() {}

  // It's usually good idea to wrap component in styled and for sake of consistency to name it <ComponentName>Styled.
  return <MyComponentStyled></MyComponentStyled>
}

// Style is kept at the bottom, inside the component file.
// This mimic structure of other popular frameworks, like Svelte.
// It allows us easy access to component's code,
// without need to scroll over style definitions, while still keeping styles
// in the same file as component itself.
const MyComponentStyled = styled.div``

// We always export default
export default  MyComponent
```

## Styling

Minimum amount of CSS in declared in `public/assets/main.css`; that's the place for general styling and to declare variables. For the rest,
`styled-components` (https://styled-components.com/) are being used.

Styles are preferably defined inside component file, at the bottom. If they grow very big, the first question should be, weather component itself is
too big, and could/should be split into multiple sections (ui elements or components). In rare cases, styles can be store in external file, called
`<ComponentName>.style.jsx` which should export one default style.

---

There should be one styled component per actual component, named `<ComponentName>Styled`. The rest of styles within that component should be tackled
with classes.

- `✅` DO:

```JSX
const MyComponentStyled = styled.div`
  .title {
    // ...
  }
  .special-section {
    // ...
  }
  input {}
`
```

This will create unique identifier for root element, but leave all sub classes named properly. So it will, in practice, generate something like:

```
.xxff .title {}
.xxff .special-section {}
.xxff input
```

This will simplify debugging CSS in code inspector, and make CSS source more readable.

- `🔴` DON'T:

```JSX
const MyComponentStyled = styled.div``
const MyComponentTitleStyled = styled.div``
const MyComponentSpecialSectionStyled = styled.div``
const MyComponentInputStyled = styled.input``
```

This makes code hard to read, and needlessly generate unique class identifiers for each element.

---

Setting properties for styled components is to be avoided, unless for setting specific value:

- `✅` DO:

```JSX
const MyComponentStyled = styled.div`
  &.big {
    font-size: var(--font-size-big);
    color: #433;
    font-weight: bold;
  }
`
```

- `🔴` DON'T (except for setting dynamic value):

```JSX
const MyComponentStyled = styled.div<{fontSize:number,color:string,fontWeight:'bold'|'normal'}>`
  font-size: ${props => props.fontSize}px;
  color: ${props => props.color};
  font-weight: ${props => props.fontWeight}px;
`
```

---

Finally you might notice that `<Divider />` elements are used throughout layouts. They serve following purposes:

- Consistent space sizes,
- visualized spacing while building a layout,
- no need to introduce additional CSS purely for margins,
- no need to introduce special CSS classes,
- easy to move and re-arrange elements without need to re-adjust margins,
- (sometimes) eliminate need for container elements,
- visible dividers (in form of lines and other shapes).

These are most useful when introducing spacing between two components, and not when introducing padding within single element.

## UI/UX

- `✅` DO: Always show busy indication when performing async action which will return results.
- `✅` DO: Catch API and other errors and show them in a friendly way.
- `✅` DO: Use hook-forms for validation and data collection.
- `🔴` DON'T: Add needlessly slow animations or transitions.
- `🔴` DON'T: Use PNG formats, when you can use SVG (especially for icons).

## API Calls

Follow easy and convenient pattern of `try-catch-finally`:

```javascript
async function fetchUsers() {
  setBusy(true)
  try {
    const [users] = await usersAPI.getAll()
    setUsers(users)
  } catch (error) {
    setError(error instanceof Error ? error.message : 'General API Error')
  } finally {
    setBusy(false)
  }
}
```

## Contributing

Contributions to Amatis food delivery are welcome and encouraged! To contribute to the project, please follow these guidelines:

1. Fork the repository and create a new branch for your changes.
2. Make your changes and test them thoroughly.
3. Ensure that your code adheres to the project's code style guidelines. The project uses ESLint for code linting, which can be run using the  npm run lint  command.
4. Ensure that your changes are well-documented and include appropriate inline comments.
5. Create a pull request and describe your changes in detail. Please include information about what your changes address and any relevant testing that you have performed.
6. Your pull request will be reviewed by the project maintainers and feedback will be provided as necessary. Once your changes have been approved, they will be merged into the main branch and included in the next release of the project.

By contributing to Amatis food delivery, you are helping to improve the project for all users and helping to build a better learning resource for frontend developers. We appreciate your

## License

The Amatis food delivery project is released under the MIT License. A copy of the license is included in the project's source code repository and can also be found below:

MIT License

Copyright (c) 2023 Amatis-raspberry

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALIN


[@Hefazi](https://github.com/hefazi)
