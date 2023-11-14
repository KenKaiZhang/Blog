# React Crash Course (Traversy Media)

Runs on the client as a **Single Page App (SPA)**, where there is a single HTML page and everything is done through React that compiles into a JavaScript bundle

Utilizes the **Virtual DOM** which updates only parts of the document that needs to be updated

Everything should be thought of as components and can be created as a...

_Function_

```js
export const Header = () => {
  return (
    <div>
      <h1>My Header</h1>
    </div>
  );
};
```

_Class_

```js
export default class Header extends React.Component {
  render() {
    return (
      <div>
        <h1>My Header</h1>
      </div>
    );
  }
}
```

...which returns/renders **JSX (JavaScript Syntac Extension)**

- allows for injection of JS data

**`npx create-react-app my-app`** will start a new React app (requires NodeJS installed)

- `npx` will cause `create-react-app` to run once instead of being installed on the system

React `dependencies`:

- **`react`**: the React library itself
- **`react-dom`**: responsible for rendering code into the DOM (browser)
- **`react-scripts`**: contains the development server, build tools, and libraries

React `scripts`:

- **`start`**: start the development server on localhost:3000
- **`build`**: build out static assets for deployment
- **`test`**: testing
- **`eject`**: expose libraries or change something in webpack

On initialization of the React project, there will be a single HTML page basically with one `div` tage with an id of `root`

In `index.js`, React inserts the application into the `root` div

All JSX elements can only be allowed one parent element

- it can be an empty tag: `<></>`

If you choose to create components using a class, they need to be `extends` with `React.Component` so they can use React life cycle methods

- React life cycle methods are functions that get called at different stages of a component's life cycle
  1. Mounting
  2. Updating
  3. Unmounting

JavaScript has a way to type hint like TypeSript with `prop-types` which will force props to be of a specific type when passed in else error the application

```js
import PropTypes from "prop-types";

export const Header = ({ title }) => {
  return (
    <div>
      <h1>{title}</h1>
    </div>
  );
};

Header.propTypes = {
  title: PropTypes.string.isRequired,
};
```
