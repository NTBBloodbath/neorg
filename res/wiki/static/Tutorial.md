<div align="center">

# Getting Started

A guide on getting started with Neorg.

</div>

## Neorg as a Concept

First of all, welcome! There's quite a journey ahead of you, hope you stick around :)

This file will get you started with Neorg as your general note taking and life management tool.

Before we get into any of the details, let us discuss what Neorg *is* and what it *isn't*. Neorg is a frontend for a markup format called norg - it provides a load
of functions for interacting with these norg files. Think of Norg files as highly advanced Markdown files (if you've ever had experience with Markdown before).

The beauty of markup is that it can contain *anything* - general documentation for your project, notes about a school subject,
technical documentation for software, theses, presentation slides... you get the idea. Because plain text is so vertasile, Neorg is built to account for as many
use cases as possible.

If you haven't encountered this type of tool before, it's officially called an *organizational tool*. The name is vague because, well, the concept is pretty vague!
Neorg is a tool that can handle any task you throw at it, as long as you can represent that problem in plaintext.

Because of this, you'll never learn *all* of Neorg, and that's okay! As you get more comfortable in a certain part of Neorg (e.g. the note-taking side or the
task management side) you can then extend your knowledge to other domains if you need.

## Our First Steps

**The first thing you'll want to do is set up Neorg**. There's an entire guide present [in the readme](https://github.com/nvim-neorg/neorg?tab=readme-ov-file#-installation)! Feel free to check it out and - once you're done - hop back into this file and get going.

Neorg is generally always active whenever you start Neovim (unless you lazy load it) - this allows you to jump to convenient locations and files whenever you need.

Before we get ahead of ourselves, let's get a feel for the default state of the plugin. By default, Neorg is merely an advanced editing tool. To see why and how, open up
any directory of your choice and open up a `note.norg` file. Ready?

## Basic Syntax

Terminology alert: **Neorg** is the name of the Neovim plugin. **Norg** is the name of the markup format that you save onto your disk. Keep this in mind as we progress!

Norg has a lot of default syntax that should immediately feel familiar if you've used `org-mode` or some Markdown. First, let's type some text:

```norg
This is my note!
```

Just like in a basic `.txt` file or like in Markdown, any text is allowed within the document.
The power of markup languages shines in the ways you can alter the text though, so let's learn some!

#### Inline Markup

Any word can be made bold, italic, underline, superscript, subscript - all through the use of modifiers. Below are a bunch of examples:

```norg
This is my note! In here I will have some *bold* text, some /italic/, _underline_, ^superscript^ and ,subscript,!
```

And indeed, upon typing those, you should see Neorg appropriately make the text **bold**, *italic* and __underline__! Superscript and subscript cannot be properly rendered
within terminals, so they're just coloured instead.

*Fantastic!* Being able to mark up any text like this without any effort is very nice.

> [!NOTE]
> If the bold, italic or underline are not showing properly you can find a troubleshooting guide [here](https://github.com/nvim-neorg/neorg/wiki/Dependencies)! Terminals can be tricky sometimes.

#### Lists

As you're writing, you'll naturally want to enumerate some things in the form of a list. Below is a simple example of a list:

```norg
Below I'll create a list of things that I should buy:
- Apples
- Oranges
- Milk
```

All it takes is to prefix a line with a `- ` and you're set! Adding more than one new line will break the list apart into two:

```norg
Below I'll create two lists of things that I should buy:
- Apples
- Oranges

- Milk
```

Apart from unordered lists, you may want to enforce an order on the list. You may be inclined to do something like this:

```norg
Below I'll create an ordered list of stuff:

1. First thing
2. Second thing
```

Nobody's stopping you from doing this, but Neorg won't recognize the list, it'll just think it's text. In norg, ordered lists are defined using the tilde (`~`):

```norg
~ First thing
~ Second thing
```

If you have the [concealer](https://github.com/nvim-neorg/neorg/wiki/Concealer) module enabled this will automatically get visually converted into a numeric list.

This approach may seem very odd initially until it clicks. When you write lists using the `1.` syntax, any time you want to add an item or reorder the list, you have to manually update *all* of the
items afterwards, or keep track of what the index of the previous item was. Let's say I have a list of 10 items, and I want to move the second item to the end. Now I have to change the numbers of all
the other entries! What if I want to add a new item at the end of the list? You have to look through the list to see what the number of the last entry was so that you can increment it by one.

Using the `~` syntax, Neorg does all of the counting for you, while still displaying the appropriate list index through the concealer. Neat!

#### Headings

As you write more complex notes you'll want to divide them up in some logical fashion. Within norg, this is done through headings:
```norg
* Shopping
  My shopping list consists of:
  - Milk
  - Butter
  - Bread
```

As you write, you may notice that Neorg will automatically indent things for you. The indentation is based on how far the heading's title is indented! For example, if you were to have this document:
```norg
*      Shopping
  My shopping list consists of:
  - Milk
  - Butter
  - Bread
```

Pressing `gg=G` (`gg` - go to top of document, `=` - indent, `G` - to the bottom of the document) will indent all of the content to match the indentation of the title!
Neorg calls this *dynamic indentation*. It can of course be tweaked.

Headings can be nested as much as you want by simply repeating the amount of asterisks!

```norg
* Shopping
** Important Shopping
   This is stuff I must immediately buy:
   - Bread
** Other Stuff
   This is not as important:
   - Milk
   - Tomatoes (yum)
```

## Next Steps: Marking Things as Tasks

Alright! We've learned how to make basic norg files, but where's the whole "organizational" part? When will I understand? One step at a time :)

You've now learned to create a basic file *somewhere* on your filesystem, and how to write some norg markup! Before we start organizing your files into meaningful places, let's learn about TODO
statuses.

Say I have a list of things I'd like to do:
```norg
- Take out the trash
- Watch "how to delete emacs" video
- Wish Mum a happy birthday
```

On its own, this is just a list... not very useful, is it? However, norg allows us to annotate *anything* within our documents as a task by giving it a TODO status:
```norg
- ( ) Take out the trash
- ( ) Watch "how to delete emacs" video
- ( ) Wish Mum a happy birthday
```

A TODO status is marked by the regular brackets right after the item itself. In our case, there's just a space inbetween the brackets - this means the task is *undone*.

Now let's say I finished watching the "how to delete emacs" video, and I would like to mark it as complete. Put your cursor on the same line as the task and press `Ctrl + Space`!
This will toggle the state of the item to "done".

> [!TIP]
> If you have the concealer enabled, this will change the task to a checkmark, but what has really happened under the hood is that
> the space has turned into an `x`! If you ever want to see the raw text of your file, run `:Neorg toggle-concealer` :)

Pressing `Ctrl + Space` again will toggle the task between three states - undone, done and pending. Pending is marked by the `-` character.

Apart from just these three states (which is what other markup formats commonly support), norg extends the amount of TODOs to a set of **twelve**!

Apart from just undone, done and pending, all of these TODO states are available:
```norg
- (=) On hold
- (_) Cancelled
- (!) Urgent
- (?) Ambiguous (uncertain)
- (+) Recurring (happens every so often)
```

To set a TODO item to a specific state you can use one of the many keybinds listed in the [`todo_items` module's wiki](https://github.com/nvim-neorg/neorg/wiki/Todo-Items#overview).

> [!NOTE]
> If you're a keen reader you will have noticed that this is nowhere near 12 TODO states.
> The others are a bit more advanced, you'll learn them as necessary!

### But Wait, There's More

Tasks aren't exclusive to lists. In norg, you can assign a task to *anything*. Not quite
done with a heading yet? No problem!

```norg
* ( ) Undone Heading
```

This will work, as will a task status attached to anything else in this fashion.

## Part Two: File Management

Now that you understand the basics of norg files and what you can put inside of them, let's give these files some meaning.

The simplest thing to get started with is writing your own diary/journal with Neorg! By default, your journal will be placed in the current working directory.
To open up the journal run `:Neorg journal today`, it should launch you into a new file!

A core concept of Neorg is the concept of *workspaces*. A workspace is a directory which contains an **index file**
(most commonly referred to as `index.norg`) in its root. This index file usually contains links to other parts in the workspace, sorted in some manner.

How do we manage such workspaces, you may ask? With `core.dirman` (short for directory manager) of course!
In your configuration, add a `core.dirman` entry as illustrated below:
```lua
require("neorg").setup({
    load = {
        ["core.defaults"] = {},
        ["core.dirman"] = {
            config = {
                workspaces = {
                    notes = "~/notes",
                },
            },
        },
    },
})
```

In that snippet we set up a list of workspaces, currently with just one workspace: `notes`.
This `notes` workspace points to, you guessed it, `~/notes`!

When in Neovim, `:Neorg workspace` will show you the current workspace you're in. This will usually be the `default` workspace - the `default` workspace
always gets created on-the-fly and points to Neovim's current working directory (seen via the `:pwd` command).

To switch to the notes workspace, run `:Neorg workspace notes`. This will switch the active workspace to `notes` and immediately drop you into its
`index.norg` file! You're free to perform any edits you may like in that workspace.

If you were working on something beforehand (e.g. some code) you may use the
`:Neorg return` command to close all norg buffers you opened since running the
`:Neorg workspace ...` command and put you right back where you started. Neat!

## To be continued...

You thought it ends here! Wrong. You've learned that Neorg is an editing mode as well as a diary writer
and a quasi file manager. Apart from this, it has many other features that are likely to be useful for a specific use case of yours.

The next parts of this tutorial are under construction... head over to either the [youtube series](https://www.youtube.com/playlist?list=PLx2ksyallYzVI8CN1JMXhEf62j2AijeDa) or 
the [list of modules](https://github.com/nvim-neorg/neorg/wiki#other-modules) to further your journey with Neorg! Have fun :)
