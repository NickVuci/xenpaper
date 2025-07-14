# craco

craco (Create React App Configuration Override) is a tool that allows you to customize the configuration of Create React App (CRA) projects without ejecting. It enables advanced tweaks to Webpack, Babel, and other build tools, which are otherwise locked down in CRA. This pattern is experimental because it bypasses the standard CRA workflow and can introduce maintenance challenges if the underlying tools change.

## How Xenpaper Uses craco

### 1. Custom Webpack Configuration

The repo uses craco to override Webpack settings, enabling features not available in vanilla CRA. For example:
- **Module resolution**: Custom aliases for easier imports between packages.
- **Monorepo support**: Adjustments to allow importing code from sibling packages in the monorepo.
- **Additional loaders**: Support for non-standard file types or advanced Babel plugins.

#### Example

See `packages/xenpaper-app/craco.config.js`:

```js
const path = require("path");

module.exports = {
    webpack: {
        alias: {
            react: path.resolve(__dirname, "../../node_modules/react"),
        },
        configure: (webpackConfig, { env, paths }) => {
            webpackConfig.module.rules[1].oneOf[2].include = [
                path.resolve(__dirname, "./src"),
                path.resolve(__dirname, "../xenpaper-ui/src"),
                path.resolve(__dirname, "../mosc/src"),
                path.resolve(__dirname, "../sound-engine-tonejs/src"),
            ];
            return webpackConfig;
        },
    },
    eslint: {
        enable: false,
    },
};
```

### 2. Babel Customization

craco allows adding Babel plugins or presets that are not included by default in CRA.

*No custom Babel plugins are currently configured in the repo's craco config, but this is a supported feature.*

### 3. Style Preprocessing

craco can be used to add support for CSS preprocessors or tweak how styled-components are handled.

*No custom style preprocessors are currently configured in the repo's craco config, but this is a supported feature.*

### 4. Monorepo Integration

craco is essential for making CRA work smoothly in a monorepo setup, allowing cross-package imports and shared dependencies. The config specifically includes sibling package source directories for transpilation.

### 5. Usage in Package Scripts

In `packages/xenpaper-app/package.json`, craco replaces the default CRA scripts to ensure custom configuration is applied:

```json
"scripts": {
  "start": "PUBLIC_URL=\"/xenpaper\" DISABLE_ESLINT_PLUGIN=true NODE_OPTIONS=--openssl-legacy-provider craco start",
  "build": "PUBLIC_URL=\"/xenpaper\" DISABLE_ESLINT_PLUGIN=true NODE_OPTIONS=--openssl-legacy-provider craco build",
  "eject": "PUBLIC_URL=\"/xenpaper\" DISABLE_ESLINT_PLUGIN=true NODE_OPTIONS=--openssl-legacy-provider craco eject"
}
```
This ensures all development, build, and test commands use the craco configuration.

### 6. Handling Monorepo Edge Cases

The craco config in `xenpaper-app` includes custom Webpack tweaks to ensure sibling packages are transpiled correctly, which is important in a monorepo setup. For example, the `include` array in the config above ensures code from sibling packages is properly transpiled and avoids issues with symlinks or hoisted dependencies.

## Discussion

Using craco is experimental because:
- It relies on internal CRA APIs, which may change and break overrides.
- Custom configs can make upgrades harder and introduce subtle bugs.
- It’s less documented and supported than standard CRA workflows.

In Xenpaper, craco was chosen to enable advanced features (monorepo, custom parsing, styled-components) without ejecting, but this comes with trade-offs in maintainability and stability.

# Critique and Alternatives

## Critique

While craco provides powerful configuration overrides for Create React App, its use introduces some risks:
- **Stability**: craco depends on internal CRA APIs, which can change without warning, potentially breaking custom configs after upgrades.
- **Community Support**: craco is less widely used and supported than vanilla CRA or more established build tools, so troubleshooting and documentation may be limited.
- **Complexity**: Custom overrides can make the build process harder to understand and maintain, especially for new contributors.

## Alternatives

For most use cases, more conventional and stable approaches include:
- **Ejecting from CRA**: This gives full control over the build setup, but at the cost of losing easy upgrades and maintenance.
- **Using Vite or Next.js**: These modern frameworks offer flexible configuration, fast builds, and strong monorepo support out of the box. Migrating to Vite or Next.js would simplify custom setups and improve long-term stability.
- **Yarn Workspaces or PNPM**: For monorepo management, these tools integrate well with Vite/Next.js and offer robust dependency handling.

## Where craco is Essential

In this codebase, craco is essential for:
- **Overriding Webpack config in a CRA app without ejecting**: This is required to support cross-package imports and transpilation in the monorepo structure.
- **Custom aliasing and transpilation of sibling packages**: These features are not possible with vanilla CRA, and ejecting would add significant maintenance overhead.

If the project remains on CRA and needs these advanced features, craco is the best available solution. If a migration to Vite or Next.js is feasible, it would provide a more stable and conventional foundation for future development.

# Refactoring Options and Recommendation

## Your Options

1. **Continue Using craco with CRA**
   - **Benefits**: No migration needed; keeps current workflow; supports advanced config without ejecting.
   - **Costs**: Risk of breakage with future CRA updates; less community support; config complexity.

2. **Eject from CRA**
   - **Benefits**: Full control over build tools and config; can solve any edge case.
   - **Costs**: Harder upgrades; more maintenance; increased complexity for contributors.

3. **Migrate to Vite or Next.js**
   - **Benefits**: Modern, fast build tools; strong monorepo support; easier config for advanced needs; large community and documentation; future-proof.
   - **Costs**: Migration effort; may require code changes; learning curve for new tools.

4. **Switch to Yarn Workspaces or PNPM for Monorepo Management**
   - **Benefits**: Better dependency management; integrates well with Vite/Next.js; scalable for larger projects.
   - **Costs**: Migration effort; may require changes to project structure.

## Recommendation

If you want long-term stability, easier upgrades, and a modern developer experience, migrating to **Vite** (for pure React) or **Next.js** (for React + SSR/routing) is recommended. These tools natively support monorepos and advanced config, reducing the need for workarounds like craco. If migration is not feasible now, continue with craco but plan for a future transition. Ejecting from CRA is only recommended if you need full control and are comfortable with increased maintenance.