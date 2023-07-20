# drsync
Fancy rsync wrapper that uses screen to do transfers in the background.

drsync (detatched rsync) is a wrapper for rsync that ingests all arguments
and then launches rsync with those arguments as a background job in a new screen
session, with the --info=progress2 option set.
Features:
  - Runs rsync with the supplied arguments with -v and --dry-run to generate the incremental
    file list, and show it to the user with less.
  - Transfer confirmation after showing the incremental file list, so if something is screwy
    there is an option to abort.
  - Includes a --non-int option that will skip all interactive elements, but retain logging
  - Logs a whole bunch of stuff including:
    - The shell command that was used to launch the job
    - Lists of source files, and the target directory/file
    - rsync dryrun incremental file list
    - Error logs on a per transfer basis
    - Cleans up file lists used to feed --include-from= and --files-from= options
      and logs their contents

Also included is a utility drsync-status, which will display the status logfile, showing the completed
percent for all active screen sessions.
  -n option lets you see the status of a particular transfer number.

findrel is a simple find wrapper that is useful for creating --files-from and --include-from file lists.

If you're using zsh, then you can add this to your .zshrc and get all of the rsync auto-completions for drsync:
compdef drsync=rsync

If you aren't using zsh what the fuck are you doing?
