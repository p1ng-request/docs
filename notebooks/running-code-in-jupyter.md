---
description: Jupyter Notebook is an interactive environment for writing and running code.
---

# Running Code in Jupyter

### Code Basics

#### `+` Insert cell below

Insert new cell below your selected cell by pressing the button `+` in the menu on the top of your notebook.

#### `✂` Remove cells

Remove cells by pressing the button `✂` in the menu on the top of your notebook.\
This button can also be used to cut your cell but it's more commonly used for removing a cell.

#### `💾` Save notebook content

Save your notebook content by pressing the button `💾` in the menu on the top of your notebook or `Control`+`S` on your hardware keyboard.

### Run Code

#### `▶︎` Run the selected cells and advanced

Code cells allow you to enter and run code.\
Run a code cell by pressing the `▶︎` button in the menu on the top of your notebook, or `Control`+`Enter` on your hardware keyboard.

```python
a = 10
print(a)
```

```
10
```

There are a couple of keyboard shortcuts for running code:

* `Control`+`Enter` run the current cell and enters command mode.
* `Shift`+`Enter` runs the current cell and moves selection to the one below.

#### `▶︎▶︎` Restart kernels and run all cells

You can reset this state by restarting the kernel with "Restart and run all cells" button.\
It will clear the kernel that maintains the state of a notebook's computations => All your variables will be lost !

### Managing the kernel

#### `⚪︎ ⚫︎` Kernel status

Code is run in a separate process called the **kernel**, which can be interrupted or restarted.\
You can see kernel indicator in the top-right corner reporting current kernel state:

* `⚪︎` means kernel is **ready** to execute code
* `⚫︎` means kernel is currently **busy**.

Tapping kernel indicator will open **kernel menu**, where you can reconnect, interrupt or restart kernel.

Try running the following cell — kernel indicator will switch from `⚪︎` to `⚫︎`, i.e. reporting kernel as "busy".\
This means that you won't be able to run any new cells until current execution finishes, or until kernel is interrupted.\


```python
import time
time.sleep(10)
```

If kernel dies you will be prompted to restart it.

#### `⬜` Interrupt the kernel

You can interrupt manually a cell execution by pressing the `⬜` button while the execution is running.\
It will stop the execution and display an error message : "KeyboardInterrupt"\


Try running the following cell and stop the execution by pressing the `⬜` button.\


```python
import time
time.sleep(30)
```

#### `↻` Restart Kernel

Restart your kernel by pressing the button `↻` in the menu on the top of your notebook
