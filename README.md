# React-Router-Dom Example(with Axios)

[:point_right: Click here to see on browser](https://react-router-dom-example.vercel.app/)

![React-Router-Dom](https://github.com/kaplanh/react-router-dom-example/assets/101884444/1a8d9d3c-874e-4bb2-a085-9ed2678aac1c)



---

| **What's used in this app ?**                                                           | **How use third party libraries** | **Author**                                                                       |
| --------------------------------------------------------------------------------------- | --------------------------------- | -------------------------------------------------------------------------------- |
| [useContext()/Context APi](https://react.dev/reference/react/useContext)                      | npm i / yarn add react-router-dom | [Take a look at my portfolio](https://kaplanh.github.io/Portfolio_with_CssFlex/) |
| [React-Router-Dom](https://reactrouter.com/en/main/start/overview)                      | npm i / yarn add react-router-dom |[Visit me on Linkedin](https://www.linkedin.com/in/kaplan-h/)   |
| [useEfect() Hook componentDidUpdate()](https://react.dev/learn#using-hooks)             |                                   |                    |
| [useState() Hook](https://react.dev/learn#using-hooks)                                  |                                   |                                                                                  |
| [fetch API](https://www.npmjs.com/package/react-fetch)         | npm i/yarn add fetch              |                                                                                  |
| [react-events](https://react.dev/learn#responding-to-events)                            |                                   |                                                                                  |
| [Bootstrap](https://getbootstrap.com/docs/5.3/getting-started/introduction/)            | npm i / yarn add bootstrap        |                                                                                  |
| [React-icons](https://react-icons.github.io/react-icons/)                               | npm i / yarn add react-icons      |                                                                                  |
| [lifting state up](https://react.dev/learn/sharing-state-between-components)              |                                   |                                                                                  |
| [props-drilling](https://react.dev/learn#sharing-data-between-components)               |                                   |                                                                                  |
| [Semantic-Commits](https://gist.github.com/joshbuchea/6f47e86d2510bce28f8e7f42ae84c716) |                                   |                                                                                  |
| Deploy with [Vercel](https://vercel.com/kaplanh)                                        |                                   |                                                                                  |
| API [reqres](https://reqres.in/api/users)      |                                   |                                                                                  |

---

## How To Run This Project 🚀

<br/>

### 💻 Install React 👇

```bash
yarn create react-app .  or npx create-react-app .
```

### 💻 Install Sass 👇

```bash
yarn add sass  or npm i sass
```

## 🔴 Delete these files and delete the imports👇

    - App.test.js
    - reportWebVitals.js
    - setupTests.js
    - favicon.ico
    - logo192.png
    - logo512.png
    - manifest.json
    - robots.txt

### 💻 Start the project 👇

```bash
yarn start or npm start
```

OR

-   <strong>Clone the Repo</strong>

    ```sh
    git clone
    ```

-   <strong>Install NPM packages</strong>

    ```sh
    npm install or yarn
    ```

-   <strong>Run the project</strong>

    ```sh
    npm start or yarn start
    ```

-   <strong>Open the project on your browser</strong>

    ```sh
    http://localhost:3000/
    ```

-   ### <strong>Enjoy! 🎉</strong>

---

## Project Skeleton

```
 React-Context-Api-example(folder)
|
|----public (folder)
│     └── index.html
|----src (folder)
|    |--- components (folder)
│    │       ├── Courses.jsx
│    │       ├── Footer.jsx
│    │       ├── Navs.jsx
│    │
|    |--- img (folder)
│    │
│    |--- pages (folder)
|    |      ├── About.jsx
|    |      ├── Home.jsx
|    |      ├── Logın.jsx
|    |      ├── People.jsx
|    |      ├── PersonDetaıl.jsx
|    |      ├── PrivateRouter.jsx
|    |
|    |--- context (folder)
│    │       ├── LoginProvider.jsx
|    |
|    |
│    ├--- App.js
│    |--- index.js
│    |--- index.css
│
│
|── .gitignore
|── package-lock.json
├── package.json
|── README.md
|── yarn.lock


```

---

### At the end of the project, the following topics are to be covered;

- useContext()/ Context Api

```jsx
//! 1.Adim

//context/LoginProvider.jsx
import { createContext, useState, useContext } from "react";

//! 1- Login Context'i olusuturuldu
const LoginContext = createContext();

//! 2-Sarmalayici (Provider) Component
const LoginProvider = ({ children }) => {
    // //! Local State
    const [user, setUser] = useState({ email: "", password: "" });

    const values = {
        user,
        setUser,
    };

    return (
        <LoginContext.Provider value={values}>{children}</LoginContext.Provider>
    );
};

//! 3- consuming custom hook
export const useLoginContext = () => {
    return useContext(LoginContext);
};

export default LoginProvider;


//! 2.adim
//App.jsx

import Footer from "./components/Footer";
import Navs from "./components/Navs";
import About from "./pages/About";
import Home from "./pages/Home";
import People from "./pages/People";
import { BrowserRouter, Routes, Route, Navigate } from "react-router-dom";
import PersonDetail from "./pages/PersonDetail";
import Login from "./pages/Login";
import LoginProvider from "./context/LoginProvider";
import PrivateRouter from "./pages/PrivateRouter";

function App() {
    return (
        <LoginProvider>
            <BrowserRouter>
                <Navs />
                <Routes>
                    <Route index element={<Home />} />
                    <Route path="about" element={<About />} />
                    <Route path="login" element={<Login />} />

                    <Route path="people" element={<PrivateRouter />}>
                        <Route path="" element={<People />} />
                        <Route path=":id" element={<PersonDetail />} />
                    </Route>

                    <Route path="*" element={<Navigate to="/" />} />
                </Routes>
                <Footer />
            </BrowserRouter>
        </LoginProvider>
    );
}

export default App;

//! 3.adim

import { Outlet, Navigate } from "react-router-dom";
import { useLoginContext } from "../context/LoginProvider";

const PrivateRouter = () => {
    const { user } = useLoginContext();
    return user?.email && user?.password ? (
        <Outlet />
    ) : (
        <Navigate to="/login" />
    );
};

export default PrivateRouter;


```
   - Nested Router
```jsx


import Nav from "../components/Nav";
import { Route, Routes } from "react-router-dom";
import Home from "../pages/Home";
import Paths from "../pages/Paths";
import People from "../pages/People";
import PersonDetail from "../pages/PersonDetail";
import Contact from "../pages/Contact";
import NotFound from "../pages/NotFound";
import Footer from "../components/Footer";
import Fullstack from "../pages/Fullstack";
import Aws from "../pages/Aws";
import Next from "../pages/Next";
import React from "../pages/React";
import PrivateRouter from "./PrivateRouter";
import Login from "../pages/Login";
import { useState } from "react";

const AppRouter = () => {
    const [user, setUser] = useState(
        JSON.parse(sessionStorage.getItem("user")) || false
    );
    return (
        <div>
            <Nav user={user} setUser={setUser} />
            <Routes>
                <Route path="/" element={<Home />} />
                <Route path="/paths" element={<Paths />}>
                    <Route index element={<Fullstack />} />
                    <Route path="fullstack" element={<Fullstack />}>
                        <Route index element={<React />} />
                        <Route path="next" element={<Next />} />
                    </Route>
                    <Route path="aws" element={<Aws />} />
                </Route>
                <Route element={<PrivateRouter user={user} />}>
                    <Route path="/people" element={<People />} />
                    <Route path="/people/:id" element={<PersonDetail />} />
                </Route>
                <Route path="/contact" element={<Contact />} />
                <Route path="/login" element={<Login setUser={setUser} />} />
                <Route path="*" element={<NotFound />} />
            </Routes>
            <Footer />
        </div>
    );
};

export default AppRouter;


```

-   Private Router

```jsx
//PrivateRouter.jsx

import { Outlet, Navigate } from "react-router-dom";
import { useLoginContext } from "../context/LoginProvider";

const PrivateRouter = () => {
    const { user } = useLoginContext();
    return user?.email && user?.password ? (
        <Outlet />
    ) : (
        <Navigate to="/login" />
    );
};

export default PrivateRouter;


```

- Login& Logout

    ```jsx
    //Nav.jsx
    import { Link } from "react-router-dom";
    import Container from "react-bootstrap/Container";
    import Nav from "react-bootstrap/Nav";
    import Navbar from "react-bootstrap/Navbar";
    import Image from "react-bootstrap/Image";
    
    import { useLoginContext } from "../context/LoginProvider";
    
    function Navs() {
        // ! Consuming login context
        const { user, setUser } = useLoginContext();

    return (
        <Navbar expand="md">
            <Container>
                <Navbar.Brand>
                    <Link className="nav-link" to="/">
                        <Image
                            width={"200px"}
                            src="https://clarusway.com/wp-content/uploads/2022/02/Adsiz-tasarim-4-1024x265.png"
                            alt="logo"
                        />
                    </Link>
                </Navbar.Brand>
                <Navbar.Toggle aria-controls="basic-navbar-nav" />
                <Navbar.Collapse id="basic-navbar-nav">
                    <Nav className="ms-auto">
                        <Link className="nav-link" to="/">
                            Home
                        </Link>
                        <Link className="nav-link" to="/about">
                            About
                        </Link>
                        <Link className="nav-link" to="/people">
                            People
                        </Link>

                        {user?.email && user?.password ? (
                            <Link
                                className="nav-link"
                                to="/login"
                                onClick={() =>
                                    setUser({ email: "", password: "" })
                                }
                            >
                                Logout
                            </Link>
                        ) : (
                            <Link className="nav-link" to="/login">
                                Login
                            </Link>
                        )}
                    </Nav>
                </Navbar.Collapse>
            </Container>
        </Navbar>
    );
   }

   export default Navs;



    ```

-   Semantic Commit Messages
    See how a minor change to your commit message style can make you a better programmer.

    Format: <type>(<scope>): <subject>

    <scope> is optional

    -   Example

    ```
                feat: add hat wobble
        ^--^  ^------------^
        |     |
        |     +-> Summary in present tense.
        |
        +-------> Type: chore, docs, feat, fix, refactor, style, or test.
    ```

-   More Examples:
    -   `feat`: (new feature for the user, not a new feature for build script)
    -   `fix`: (bug fix for the user, not a fix to a build script)
    -   `docs`: (changes to the documentation)
    -   `style`: (formatting, missing semi colons, etc; no production code change)
    -   `refactor`: (refactoring production code, eg. renaming a variable)
    -   `test`: (adding missing tests, refactoring tests; no production code change)
    -   `chore`: (updating grunt tasks etc; no production code change)

---

## Feedback and Collaboration

I value your feedback and suggestions. If you have any comments, questions, or ideas for improvement regarding this project or any of my other projects, please don't hesitate to reach out.
I'm always open to collaboration and welcome the opportunity to work on exciting projects together.
Thank you for visiting my project. I hope you have a wonderful experience exploring it, and I look forward to connecting with you soon!

<p align="center"> ⌛<strong> Happy Coding </strong> ✍ </p>
