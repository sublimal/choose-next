# choose-next

Chooses a file from a directory. Very handy to re-watch tv series!

## Motivation

Sometimes (when recovering from a hangover, being depressed, etc.)
all you want is to lie in bed an watch a few Futurama/Malcolm episodes.
But even navigating to the right folder and choosing an episode which
you haven't seen yesterday is too much work.

With this small and simple script all you have to do is to type "playfuturama"
(using tab completion of course!) if you have set up e.g. this alias:

    alias playfuturama='choose-next -c "mplayer -fs" "/media/usb/Futurama"'


## Usage

    Usage: choose-next [OPTION]... DIR [FILE]...
    
    Chooses a file from directory DIR (recursively) and print it's name to stdout.
    Afterwards it is appended to a log file. Only files which are not in log file
    are considered for selection. Tries to choose the file which is next in
    lexical order in DIR.
    
    Options:
      --version             show program's version number and exit
      -h, --help            show this help message and exit
      -c CMD, --command=CMD
                            execute CMD on every selected file; %s in CMD is
                            substituted with the filename, otherwise it is
                            appended to CMD
      --clear               remove log file and exit
      --clear-first         remove first log file entry and exit
      --clear-last          remove last log file entry and exit
      --dump                dump log file to stdout and exit
      -i, --no-read         don't use log file to filter selection
      -L FILE, --logfile=FILE
                            path of log file (default:
                            ~/.choose-next/${DIR//\//_})
      -l, --last            play last played file
      -n NUM, --number=NUM  number of files to select (-1: infinite)
      -p, --prepend         prepend selected filename instead of appending
      -q, --quiet           don't output anything
      -r, --random          choose a random file from DIR
      -v, --verbose         be verbose (can be used multiple times)
      -w, --no-write        don't record selected files to log file


## Examples

Over the next few weeks you want to watch all Futurama episodes in strict
rotation:

    # clear existing log file
    choose-next --clear /media/usb/Futurama
    # no special options needed
    alias playfuturama='choose-next -c "mplayer -fs" "/media/usb/Futurama"'

You want to see a random episode (out of order!), but not one you have already
seen. You want to prepend the filename so that the rotation order is retained:

    playfuturama -rp

You were somehow distracted, and want to watch the last episode again:

    playfuturama -l

You want to watch a specific episode, and continue to watch from this point on:

    playfuturama -n10 "/media/usb/Futurama/S04E01.avi"
