# Diffs for "Add stack-auth to web project" Pull Request

Below are the diffs for the first two files changed in the PR to add stack-auth integration:

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

---

For more details or additional diffs, see the PR or request a specific file.
