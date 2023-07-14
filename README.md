# react-frontend-template

## 1. Install base Package

```
pnpm create vite . --template react 
pnpm add react-router-dom
pnpm add react-redux @reduxjs/toolkit
pnpm add axios
 pnpm add react-toastify
```
## 2. Install Tailwind CSS
Install tailwindcss via npm, and then run the init command to generate your tailwind.config.js file.

```
pnpm add -D tailwindcss postcss autoprefixer
pnpm exec tailwindcss init -p
```

## 3. Configure your template paths
Add the paths to all of your template files in your tailwind.config.js file.
```
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./src/**/*.{js,jsx,ts,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

## 4. Add the Tailwind directives to your CSS 
Add the @tailwind directives for each of Tailwind’s layers to your ./src/index.css file.

```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## 5. Start using Tailwind in your project
Start using Tailwind’s utility classes to style your content.

```
export default function App() {
  return (
    <h1 className="text-3xl font-bold underline">
      Hello world!
    </h1>
  )
}
```


https://tailwindcss.com/docs/guides/create-react-app

## 6 Run

```
pnpm run dev
```