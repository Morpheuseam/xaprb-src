---
title: How to install beautiful X11 cursors
date: "2006-04-24"
url: /blog/2006/04/24/beautiful-x11-cursors/
categories:
  - Desktop
---
X11 comes with unattractive mouse cursors, but it's trivial to replace them with other themes. In this article I'll explain how to install mouse cursors system-wide or for a single user, and give you links to my favorite cursor themes.

Nicely crafted mouse cursors are very important for usability, in my opinion. I need my mouse cursors to be unobtrusive, yet really easy to see. They need to be easy to find without peering at the screen or waving the mouse wildly, and easy to use precisely on every kind of background. Smooth, beautiful cursors are a definite plus.

Themes are supported in [XFree86](http://www.xfree86.org/) 4.3 or newer. All versions of [xorg](http://www.x.org/), the successor to XFree86, support themes. I hope you're using xorg by this time.

### Available mouse cursor themes

Many themes are available---a great site to look for them is [KDE look](http://www.kde-look.org/?xcontentmode=36). In my opinion, and this is only my opinion, most cursor themes are something only a mother could love. I don't even like the "high-quality" cursors packaged specifically for Gentoo.

Then again, maybe I'm not like most folks. I like very minimal and functional things with as little clutter as possible. When I look at screenshots of other people's desktops cluttered with a million windows and root-tail displays, transparent terminals and a huge gkrellm window along the side displaying system load, all I can think of is attention deficit disorder. I like [XFCE](http://www.xfce.org) with nothing but a taskbar showing, or [Fluxbox](http://fluxbox.sourceforge.net), or even [Ratpoison](http://www.nongnu.org/ratpoison/). Heck, I'm happy with just a terminal and a [screen](http://www.gnu.org/software/screen/) session. But, that's just me.

I digress---back to beautiful cursors. I think the [neutral cursor theme](http://www.kde-look.org/content/show.php?content=28310) is very nice, but I like the [Red Hat 9 cursors](http://www.kde-look.org/content/show.php?content=5600) even better. The I-beam is thinner, the default arrow has a single-pixel black tip when in front of a white background for precision, and the busy cursor is less distracting. On the plus side, both themes are very straightforward and plain, yet highly attractive and usable.

If you like the looks of these but prefer colorful cursors, the [jaguarx cursor theme](http://www.kde-look.org/content/show.php?content=6679) is very similar, but has color added. And if you want to mix and match cursors from different themes, well, they're just files---make your own! It's really easy.

These themes are licensed under the GPL, so I'm free to redistribute them, a liberty I'm happy to take. I've provided links below for your convenience:

1.  [Neutral cursor theme](/media/2006/04/neutral.tar.gz)
2.  [Another (older?) version of the neutral cursor theme](/media/2006/04/neutral-old.tar.gz)
3.  [Red Hat 9 cursor theme](/media/2006/04/redhat9cursors.tar.gz)
4.  [Jaguarx cursor theme](/media/2006/04/jaguarx.tar.gz)

### Installation options

There are three basic ways to install the themes:

1.  System-wide
2.  System-wide in the local directory
3.  For one user only

System-wide installations place the cursors in subdirectories of `/usr/share/cursors/xorg-x11`. System-wide in the local directory means placing them in `/usr/local/share/cursors/xorg-x11`. The difference is `/usr/share/` installations will get cleaned out by installation and package management systems, so unless you install them through your distribution's package management system, you may lose them when upgrading X11. `/usr/local/share` installations won't get wiped out when upgrading your system.

Single-user installations require no access to system directories, so a non-root user can alter his or her own theme easily, and even take it from computer to computer. In this case, the themes are placed in subdirectories in `~/.icons/`.

User-specific settings override local settings, which override system-wide settings.

### Installing the theme

To install a theme, download the theme and unpack it. You should have a directory structure like the following:

*   theme_name 
    *   index.theme
    *   cursors 
        *   cursor files...

Move the entire `theme_name` directory to the installation destination: `/usr/share/cursors/xorg-x11/`, `/usr/local/share/cursors/xorg-x11/`, or `~/.icons/`.

In Gentoo, you can install packages from Portage as usual: `emerge blueglass-xcursors`.

### Choosing a default theme

There's a concept of a default theme. The default theme is located in the `default/` subdirectory of wherever you've installed your theme. This is how the system decides which theme to use---it uses the "default" theme. It reads the `index.theme` file and looks at it.

If you installed your theme system-wide or system-wide local, you need to edit the `/usr/share/cursors/xorg-x11/default/index.theme` or the `/usr/local/share/cursors/xorg-x11/default/index.theme` file. Specify the default theme should **inherit from** the theme you want to use. For example, here is the default X11 theme if you haven't specified anything else:

```
[Icon Theme]
Inherits=core
```

That file tells X11 to use the `core` cursor theme---the one built right into X11 itself. If you want to use the `neutral` theme instead, edit the file thusly:

```
[Icon Theme]
Inherits=neutral
```

If you installed the theme in your `~/.icons/` directory, you can do several different things:

*   Rename the theme directory from `theme_directory` to `default`.
*   Leave your themes in their original directories, and make a `default` directory and create in it a single file called `index.theme` with the contents as shown just above.
*   Leave your themes in their original directories, and make a symlink named `default` to the theme directory. For instance, `ln -sfnT ~/.icons/redhat9cursors/ ~/.icons/default`.

I like the last option, because it never leaves me in doubt about which theme I'm really using.
    
**Update: in Ubuntu Hardy Heron, open System/Preferences/Appearance and click "Customize..." then select the Pointer tab. Select your preferred cursor set here. The list will include cursors installed under ~/.icons/**


