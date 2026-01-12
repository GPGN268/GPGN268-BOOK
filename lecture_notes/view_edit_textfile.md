# Viewing and editing text files (cat and VIM)

## Learning Objectives
- Create and edit files using an editor
- Check the content of a text file using cat, head, tail, and wc

## Checking the content of a file

We can use the `cat` command to quickly view the content of a plain text file. For example:

```shell
$ cat README.md
```

This prints the entire file content to the screen, which is not ideal for large files. For a partial view, use `head` and `tail`.

```shell
$ head 372-U1520B_den-nscope.csv
```

`head` displays the first few lines of a file, while

```shell
$ tail 372-U1520B_den-nscope.csv
```

`tail` displays the last few lines. 

You can also specify how many lines you would like to see using the flag `-n`

```shell
$ tail -n 10 372-U1520B_den-nscope.csv
```

```shell
$ head -n 2 README.md 
```

Another simple task that might be handy is to count how many lines there are in a file. 

```shell
$ wc README.md
4    11    90    README.md
```

The `wc` command displays the total number of lines, words, and bytes for the input (in this case, `README.md`).

## Creating files

**Which editor?**
For this part of the lecture, we will learn the basics of a text editor called [Vim](https://www.vim.org/). The first thing that you might ask is "Do I really need to learn this? It seems pretty outdated..." I have been using Vim since I started coding as an undergrad just like you. I could spend a whole lecture convincing you that should still use Vim even when there are many modern text editors available (such as [VS Code](https://code.visualstudio.com/), [Sublime](https://www.sublimetext.com/), and [Notepad++](https://notepad-plus-plus.org/)), but I won't. Instead, I will share a few reasons why **I** use Vim. 
- **Vim is always available.** I do most of my work on remote machines, which operate on Linux and where I have no [graphical user interface](https://en.wikipedia.org/wiki/Graphical_user_interface) (GUI) to interact with, and no permission to install programs. Knowing Vim means that I can write code and edit files in the same way, no matter where I'm working. 
- **Vim has been around for 3 decades and ain't going anywhere.** While modern text editors and [IDEs](https://en.wikipedia.org/wiki/Integrated_development_environment) have several cool features that can make writing coding and editing text very efficient, in technology, tools hardly stick around for long. I don't want to invest time and energy learning all the tricks of a particular text editor when the chances that it will eventually stop working are pretty high (as it's the case for [Atom](https://github.blog/2022-06-08-sunsetting-atom/)).
- **Vim saves me time**. Vim is light and fast. There is basically no latency for opening and editing files. It is also highly customizable without the need of installing anything extra. Most importantly, once I learned the basics of Vim and build some muscle-memory it's nearly impossible for me to be as efficient using something else.

In this course, you will need some basic Vim skills, so this is what we will focus on. No matter what career path you choose, using Vim to open a file, add and delete text, and save it is something that will be useful to know. Advanced Vim can be extremely powerful and I encourage you to check out this [Vim cheat sheet](http://www.viemu.com/a_vi_vim_graphical_cheat_sheet_tutorial.html), the [official Vim documentation](https://www.vim.org/docs.php) as well as this [interactive Vim tutor](https://www.openvim.com/) if you are interested in learning more.

## Getting started with vim 
Now let's navigate to our data directory and create a text file using Vim.

```
$ cd iodp-logging-data
$ vim README.md
```

The syntax `$ vim filename` can be used to create or open an existing file, where `filename` represents the target file you want to create or modify. The most important thing about Vim is that it has multiple modes. Here are three that we will use in this course:

| Mode    | Description                                 |
| ------- | ------------------------------------------- |
| Normal  | Default; for navigation and simple editing  | 
| Insert  | For explicitly inserting and modifying text |
| Command | For operations like saving, exiting, etc.   |

If you try to type, nothing will happen because Vim is in its default mode (normal). To be able to type, we switch to " insert" mode by typing `i`, which stands for " insert". Let's go ahead and try to type some information about our data. 

``` Markdown
## General information
last modified: YYYY-MM-DD
date created: YYYY-MM-DD
author: Blaster
## Dataset Information
- General Description: files containing well-logging data from the International Ocean Drilling Program (IODP)
```

Now, to go back to normal mode we hit `esc`. Now, we would like to save our file. To do that, we enter ` :` to go to command mode. Note that a colon appeared at the bottom of the page. This indicates that Vim is ready for our command. In this case, we want to "write" (which is the same as save) and the command for that is `w`. To run the command we hit "return" To exit vim we run `q`, from "quit". 

Now, if you run
```
$ ls -F
```

you should see the file that we just created.