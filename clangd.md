# Patch nvim-lspconfig for clangd

Apply the following patch to `~/.local/share/nvim/lazy/nvim-lspconfig/lsp/clangd.lua`

```
diff --git a/lazy/nvim-lspconfig/lsp/clangd.lua b/lazy/nvim-lspconfig/lsp/clangd.lua
index d0f01d3..5198a84 100644
--- a/lazy/nvim-lspconfig/lsp/clangd.lua
+++ b/lazy/nvim-lspconfig/lsp/clangd.lua
@@ -61,7 +61,14 @@ end
 ---@field offsetEncoding? string
 
 return {
-  cmd = { 'clangd' },
+  cmd = {
+    'clangd',
+    '--background-index',
+    '--header-insertion=never',
+    '--completion-style=detailed',
+    '--function-arg-placeholders',
+    '--fallback-style=llvm',
+  },
   filetypes = { 'c', 'cpp', 'objc', 'objcpp', 'cuda', 'proto' },
   root_markers = {
     '.clangd',
@@ -78,7 +85,8 @@ return {
         editsNearCursor = true,
       },
     },
-    offsetEncoding = { 'utf-8', 'utf-16' },
+    --offsetEncoding = { 'utf-8', 'utf-16' },
+    offsetEncoding = { 'utf-8' },
   },
   ---@param client vim.lsp.Client
   ---@param init_result ClangdInitializeResult
```

