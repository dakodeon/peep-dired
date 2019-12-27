# NOTES

- Peep dired is a very useful tool for my workflow, but I feel some features are missing, like a more integrated experience (e.g. functions like dired-prev/next-dir don't have an equivalent). I fixed some of these issues in my config, but it would be nice to be part of peep.
- I have to work out what happens with cleanup-on-disable which stopped working and with cleanup-eagerly that never worked correctly.
- A very useful feature would be the execution of some external script to be shown instead of the file for ignored extensions (e.g. thumbnails for video files --check image-dired, or mp3 tags for mp3 files etc)
- Another thing: maybe quit peep dired when no peep buffer is visible
- Navigation: if peep is enabled in a directory whose parent or child is already open and has not peep enabled, navigating to this directory should enable peep.
- Minor detail: Change defaults for scrolling other window, since using SPC and DEL conflicts with Wdired

dakodeon 20191227

# This project is looking for a mainater, please look [here](https://github.com/asok/peep-dired/issues/17)

# Peep Dired

This is a minor mode that can be enabled from a dired buffer.
Once enabled it will show the file from point in the other window.
Moving to the other file within the dired buffer with <kbd>down</kbd>/<kbd>up</kbd> or
<kbd>C-n</kbd>/<kbd>C-p</kbd> will display different file.
Hitting <kbd>SPC</kbd> will scroll the peeped file down, whereas
<kbd>C-SPC</kbd> and <kbd>backspace</kbd> will scroll it up.

![Screenshot](https://github.com/asok/peep-dired/raw/master/screenshots/peep-dired-cast.gif)

## Installation

Once you have setup [Melpa](http://melpa.milkbox.net/#/getting-started) you can use `package-install` command to install Peep Dired. The package name is `peep-dired`.

## Configuration

### Customizing

When disabling the mode you can choose to kill the buffers that were opened while browsing the directories.
```el
(setq peep-dired-cleanup-on-disable t)
```

Or you can choose to kill the buffer just after you move to another entry in the dired buffer.
```el
(setq peep-dired-cleanup-eagerly t)
```

If you want the dired buffers that were peeped to have the mode enabled set it to true.
```el
(setq peep-dired-enable-on-directories t)
```

### Evil integration
Adjust the state name depending on an evil state you open dired in:

```
(evil-define-key 'normal peep-dired-mode-map (kbd "<SPC>") 'peep-dired-scroll-page-down
                                             (kbd "C-<SPC>") 'peep-dired-scroll-page-up
                                             (kbd "<backspace>") 'peep-dired-scroll-page-up
                                             (kbd "j") 'peep-dired-next-file
                                             (kbd "k") 'peep-dired-prev-file)
(add-hook 'peep-dired-hook 'evil-normalize-keymaps)
```

## Ignoring Certain File Extensions

You probably don't want to open certain files like videos when using Peep Dired. To ignore certain files when moving over them you can customize the following to your liking:

```
(setq peep-dired-ignored-extensions '("mkv" "iso" "mp4"))
```

## Alternatives

* [ranger.el](https://github.com/ralesi/ranger.el) emulates [ranger](http://ranger.nongnu.org/) in dired. It has the preview feature similar to Peep-Dired.

## Contribution

Install [cask](https://github.com/rejeep/cask.el) if you haven't already, then:

```bash
$ cd /path/to/peep-dired
$ cask
```

Run all tests with:

```bash
$ make test
```
