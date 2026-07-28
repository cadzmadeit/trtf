# Shopify Theme Development Rules

1. **Never Inject Inline `<style>` Blocks**: Do not inject messy `<style>` blocks directly into `.liquid` files to force layouts. Always locate the corresponding `assets/*.css` file and append custom rules cleanly there.
2. **Respect Javascript Sliders (Swiper)**: Never brute-force CSS like `display: flex !important` or `overflow-x: auto` on Swiper containers (`.swiper-wrapper`). It breaks the Javascript calculations. Check `global.js` or `product-single.js` to modify the Swiper initialization parameters (like `direction: horizontal`) instead.
3. **Never Mutate Files with Brittle Python Scripts**: Do not use Python `split()` or regex to hack large `.liquid` files. It risks destroying critical `{% schema %}` blocks. Use the exact `replace_file_content` tool with precise line numbers to guarantee safe edits.
4. **Always Verify Schema**: After making any edits to a Shopify `.liquid` section, always ensure the `{% schema %}` block at the bottom remains intact. If it is deleted, Shopify will fail to render the section's blocks.
5. **Use Strict Tools**: Strictly use `grep_search` for searching and `view_file` for reading code. Avoid hacking together `cat`, `grep`, or `sed` in bash commands, as they lead to dangerous and unintended file modifications.
