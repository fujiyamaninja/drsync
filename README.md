# drsync
Fancy rsync wrapper that uses screen to do transfers in the background.

drsync (detatched rsync) is a wrapper that uses screen to do file transfer operations in the background.
All arguments are passed through to rsync, and all transfers are run with --info=progress2. Using screen 
to conduct the transfers in this way allows transfers to happen in the background, while still providing
a way to see the percent completed with --info=progress2. This is very useful for large, hours long
transfers where you want to be able to monitor the progress.

Features:
  - Logs and displays incremental file list in less from a dry-run before launching any screen sessions.
  - Option to abort transfer after viewing the incremental file list, in case there is a problem with the files selected.
  - Includes a --non-int option that will skip display and confirmation of the file list, but retain logging.
  - Logs a whole bunch of stuff including:
    - The shell command that was used to launch the job
    - Lists of source files, and the target directory/file
    - rsync dry-run incremental file list
    - Error logs on a per transfer basis
    - Cleans up file lists used to feed --include-from= and --files-from= options
      and logs their contents
  - All logs are stored in ~/.drsync_transfers/. This directory is safe to remove. It will be regenerated and start logging again with transfer number 1 if it does not exist.

Also included is a utility drsync-status, which will display the status logfile, showing the completed
percent for all active screen sessions.
-n option lets you see the status of a particular transfer number.

findrel is a simple find wrapper that is useful for creating --files-from and --include-from file lists.

If you're using zsh, then you can add this to your .zshrc and get all of the rsync auto-completions for drsync:

compdef drsync=rsync

If you aren't using zsh what the fuck are you doing?
