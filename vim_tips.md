# **Neovim/Vim Tips & Tricks**  
*A guide for editing, navigation, plugins, and Verilog workflows.*  

---

## **Table of Contents**  
1. [File Operations](#file-operations)  
2. [Navigation](#navigation)  
3. [Splits & Tabs](#splits--tabs)  
4. [Search & Replace](#search--replace)  
5. [Commenting](#commenting)  
6. [Verilog-Specific](#verilog-specific)  
7. [Plugins](#plugins)  
8. [Diff Tools](#diff-tools)  
9. [Clipboard](#clipboard)  

---

## **File Operations**  
### **Create/Save Files**  
```vim
:enew                 " Create new buffer  
:w filename.txt       " Save as filename.txt  
:wq or :x             " Save and quit  
:q!                   " Quit without saving  
```

### **Open Existing Files**  
```vim
:e path/to/file.txt   " Open file in current buffer  
:Ex                  " Open file explorer  
```

---

## **Navigation**  
### **Basic Movement**  
```vim
h, j, k, l            " Left, Down, Up, Right  
w, b                  " Next/previous word  
0, $                  " Start/end of line  
gg, G                 " Top/bottom of file  
Ctrl + u, Ctrl + d    " Half-page up/down  
```

### **Jump to Definitions**  
```vim
gd                    " Go to definition (LSP)  
Ctrl + ]              " Jump to tag (ctags)  
gr                    " Find references (LSP)  
```

### **Fuzzy Search**  
*(Requires [Telescope](https://github.com/nvim-telescope/telescope.nvim))*  
```vim
:Telescope find_files " Search files  
:Telescope live_grep  " Search text in files  
```

---

## **Splits & Tabs**  
### **Window Splits**  
```vim
:sp file.txt          " Horizontal split  
:vsp file.txt         " Vertical split  
Ctrl + w + h/j/k/l    " Move between splits  
Ctrl + w + c          " Close split  
```

### **Tabs**  
```vim
:tabnew file.txt      " Open in new tab  
gt, gT                " Next/previous tab  
```

---

## **Search & Replace**  
```vim
/pattern              " Search forward  
?pattern              " Search backward  
n, N                  " Next/previous match  
:%s/old/new/g         " Replace all  
```

---

## **Commenting**  
### **Built-in**  
```vim
:s/^/\/\/             " Comment line (Verilog)  
:s/^\/\///            " Uncomment  
```

### **Plugins**  
- **Comment.nvim**:  
  ```vim
  gcc                  " Toggle line comment  
  gbc                  " Toggle block comment  
  ```
- **vim-commentary**:  
  ```vim
  gcc                  " Toggle comment  
  ```

---

## **Verilog-Specific**  
### **LSP Setup**  
```lua
-- init.lua  
require('lspconfig').verible.setup{}  
```
**Keymaps**:  
- `gd`: Go to definition  
- `K`: Hover documentation  

### **Tags Navigation**  
```sh
ctags -R --languages=verilog  " Generate tags  
```
```vim
Ctrl + ]              " Jump to tag  
```

### **Waveform Debugging**  
```sh
:!gtkwave waveform.vcd  
```

---

## **Plugins**  
### **Essential Plugins**  
```lua
-- Packer.nvim  
use {  
  'numToStr/Comment.nvim',       " Commenting  
  'nvim-telescope/telescope.nvim', " Fuzzy search  
  'sindrets/diffview.nvim',      " Diff tools  
}  
```

---

## **Diff Tools**  
### **Built-in Diff**  
```sh
nvim -d file1.v file2.v  
```
**Commands**:  
```vim
]c, [c               " Next/previous diff  
:diffupdate          " Refresh diff  
```

### **Diffview.nvim**  
```vim
:DiffviewOpen file1.v file2.v  
```

---

## **Clipboard**  
### **Pasting in Neovide**  
- `Ctrl + Shift + V`: Paste from system clipboard.  
- `"+p`: Paste from Neovim’s clipboard.  

### **Fix Clipboard**  
```sh
sudo apt install xclip  # Linux  
```

---

## **Pro Tips**  
- **Reload Config**: `:luafile %`  
- **Check Filetype**: `:set ft?`  
- **Custom Keymaps**: Add to `init.lua`:  
  ```lua
  vim.keymap.set('n', '<leader>ff', ':Telescope find_files<CR>')  
  ```

---

**Enjoy your Neovim journey!** 🚀  
