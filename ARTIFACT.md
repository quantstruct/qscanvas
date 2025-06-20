# File Paths and Diffs for "Add stack-auth to web project" PR

This PR introduces the following changes:

---

## 1. apps/web/package.json (modified)
```diff
@@ -64,6 +64,7 @@
     "@radix-ui/react-toast": "^1.2.2",
     "@radix-ui/react-tooltip": "^1.1.7",
     "@replit/codemirror-lang-csharp": "^6.2.0",
+    "@stackframe/stack": "^2.7.21",
     "@supabase/ssr": "^0.5.1",
     "@supabase/supabase-js": "^2.45.5",
     "@types/react-syntax-highlighter": "^15.5.13",
```
_Adds the `@stackframe/stack` dependency._

---

## 2. apps/web/src/app/handler/[...stack]/page.tsx (added)
```diff
@@ -0,0 +1,6 @@
+import { StackHandler } from "@stackframe/stack";
+import { stackServerApp } from "../../../stack";
+
+export default function Handler(props: unknown) {
+  return <StackHandler fullPage app={stackServerApp} routeProps={props} />;
+}
```
_New file: handler page using StackHandler and stackServerApp._

---

## 3. apps/web/src/app/layout.tsx (modified)
```diff
@@ -1,4 +1,6 @@
 import type { Metadata } from "next";
+import { StackProvider, StackTheme } from "@stackframe/stack";
+import { stackServerApp } from "../stack";
 import "./globals.css";
 import { Inter } from "next/font/google";
 import { cn } from "@/lib/utils";
@@ -19,7 +21,7 @@ export default function RootLayout({
 }) {
   return (
     <html lang="en" className="h-screen">
-      <body className={cn("min-h-full", inter.className)}>{children}</body>
+      <body className={cn("min-h-full", inter.className)}><StackProvider app={stackServerApp}><StackTheme>{children}</StackTheme></StackProvider></body>
     </html>
   );
 }
```
_Adds StackProvider and StackTheme; wraps children with stack context._

---

## 4. apps/web/src/app/loading.tsx (added)
```diff
@@ -0,0 +1,5 @@
+export default function Loading() {
+  // Stack uses React Suspense, which will render this page while user data is being fetched.
+  // See: https://nextjs.org/docs/app/api-reference/file-conventions/loading
+  return <></>;
+}
```
_New file: loading component for React Suspense._

---

## 5. apps/web/src/stack.tsx (added)
```diff
@@ -0,0 +1,7 @@
+import "server-only";
+
+import { StackServerApp } from "@stackframe/stack";
+
+export const stackServerApp = new StackServerApp({
+  tokenStore: "nextjs-cookie",
+});
```
_New file: exports stackServerApp._

---

## 6. yarn.lock (modified)
_(1631 additions, 32 deletions; large lockfile diff omitted for brevity)_

---

If you need the full diff for yarn.lock or further details on any file, let me know!
