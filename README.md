# Theme switching

A Kelor Block that adds light and dark themes to a Next.js app with [next-themes](https://github.com/pacocoursey/next-themes).

It is made for the [Next.js Base](https://github.com/kelor-examples/example-next-base), and works with any Next.js Base that has a provider list in `src/app/providers.tsx` with the standard `// kelor:imports` and `// kelor:wrappers` placeholders. It combines with other Blocks that add providers there.

## What it adds

- `src/components/theme-provider.tsx`: next-themes' `ThemeProvider`, set to put the theme's name in the `class` of `<html>` and to follow the system theme until the user picks one.
- The `next-themes` package in `package.json`.
- In `src/app/providers.tsx`: the import, and `ThemeProvider` in the provider list, so it wraps every page.

The Base's `<html>` needs `suppressHydrationWarning`, because next-themes sets its class before React loads. The Next.js Base has it.

## Use it

Read or change the theme from any client component:

```tsx
"use client";

import { useTheme } from "next-themes";

export function ThemeToggle() {
  const { resolvedTheme, setTheme } = useTheme();
  return (
    <button onClick={() => setTheme(resolvedTheme === "dark" ? "light" : "dark")}>
      Toggle theme
    </button>
  );
}
```

To make Tailwind CSS's `dark:` classes follow the chosen theme rather than the system setting, add this line after `@import "tailwindcss";` in `src/app/globals.css`:

```css
@custom-variant dark (&:where(.dark, .dark *));
```
