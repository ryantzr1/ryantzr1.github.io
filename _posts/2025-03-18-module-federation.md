---
layout: post
title: "Module Federation: Streamlining Code Sharing in Web Development"
date: 2025-03-18 10:00
categories: [frontend]
tags: [webpack, module-federation, microfrontends, javascript, code-sharing]
description: "Discover how Module Federation elegantly solves code sharing challenges in web development by enabling applications to dynamically share components and libraries without duplication or complex microservices."
repo: https://github.com/webpack/webpack
website: https://webpack.js.org/concepts/module-federation
---

Sometimes, the best way to manage shared code across applications isn’t through duplication or complex microservices—it’s by letting applications dynamically borrow what they need. Let’s explore how **Module Federation** tackles this elegantly.

---

## The Problem

Modern web development often involves multiple applications that share components or libraries. Traditionally, this leads to:

- **Code duplication**: Each app bundles its own copy of shared dependencies (e.g., React, UI components).
- **Maintenance headaches**: Updating a shared library requires changes across every app that uses it.
- **Slower performance**: Bloated bundle sizes increase load times.
- **Team coordination issues**: Independent teams struggle to sync shared code updates.

Imagine two apps using the same modal component. Without Module Federation, updating the modal means redeploying both apps—a tedious and error-prone process.

---

## Before and After

### Before Module Federation

Developers relied on:

1. **Monoliths**: A single codebase for all features (simple but unwieldy).
2. **Microservices**: Independent services with complex coordination.
3. **Manual copying**: Error-prone and hard to scale.

### After Module Federation

Applications act as **hosts** (consumers) or **remotes** (providers), sharing code dynamically. For example:

- A **remote** app exposes a shared `Button` component.
- A **host** app imports `Button` from the remote, avoiding duplication.

---

## Ways to Solve the Problem: A Comparison

| Approach              | Pros                                | Cons                         |
| --------------------- | ----------------------------------- | ---------------------------- |
| Monolith              | Simple management                   | Inflexible, scales poorly    |
| Microservices         | Independent deployment              | Complex communication        |
| **Module Federation** | **Dynamic sharing, faster updates** | **Initial setup complexity** |

---

## Why Choose Module Federation?

### Pros

- **Eliminate duplication**: Share libraries/components across apps.
- **Improve performance**: Load shared code once, reducing bundle sizes.
- **Simplify maintenance**: Update shared code in one place.
- **Team-friendly**: Decentralized development without coordination chaos.

### Cons

- **Learning curve**: Requires understanding Webpack configuration.
- **Setup effort**: Initial orchestration of hosts/remotes.

**Unexpected Benefit**: Teams find debugging easier, as shared modules are versioned and tracked centrally.

---

## How to Use Module Federation

### Basic Setup with Webpack

1. **Remote App Configuration** (exposes components):

```javascript
// webpack.config.js (Remote)
const { ModuleFederationPlugin } = require("webpack").container;

module.exports = {
  plugins: [
    new ModuleFederationPlugin({
      name: "remote_app",
      filename: "remoteEntry.js",
      exposes: {
        "./Button": "./src/components/Button.js",
      },
      shared: ["react", "react-dom"],
    }),
  ],
};
```

2. **Host App Configuration** (consumes the remote):

```javascript
// webpack.config.js (Host)
const { ModuleFederationPlugin } = require("webpack").container;

module.exports = {
  plugins: [
    new ModuleFederationPlugin({
      name: "host_app",
      remotes: {
        remote_app: "remote_app@http://localhost:3001/remoteEntry.js",
      },
      shared: ["react", "react-dom"],
    }),
  ],
};
```

3. **Using the Shared Component in React**:

```javascript
// HostApp.js
const Button = React.lazy(() => import("remote_app/Button"));

const App = () => (
  <React.Suspense fallback="Loading Button...">
    <Button />
  </React.Suspense>
);
```

**Pro Tip**: Tools like [Rspack](https://rspack.dev) simplify configuration with built-in Module Federation support.

---

Module Federation is a game-changer for teams building scalable, maintainable web apps. It’s ideal for:

- **Microfrontends**: Independent teams owning app parts.
- **Large codebases**: Reduce redundancy and speed up load times.
- **Dynamic updates**: Propagate changes instantly across apps.

While smaller projects might find the setup cumbersome, the long-term benefits for collaboration and performance are undeniable. Future updates, like enhanced DevTools integration, will make it even more powerful.

---

**Further Readings**

- [Module Federation Official Documentation](https://module-federation.io/guide/start/index.html)
- [Real-World Experiences](https://github.com/module-federation/module-federation-examples)
- [Rspack: A Rust-Powered Web Bundler](https://rspack.dev)
