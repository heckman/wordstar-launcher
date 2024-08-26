# Change Log

## Version 0.5.1

- Bugfixes to `zsh` version.

## Version 0.5.0

- Use `zsh` as the script's interpreter.

## Version 0.4.2

- Change the default behaviour to allow documents at any path to be opened.
  This exposes their parent directory to _DOSBox-X_ and _WordStar_.

## Version 0.4.1

- Change command-line options. This is a breaking change.
- Rename variables for clarity.

## Version 0.4.0

- Added `wordstar -a` option to allow a document at any path
  to be opened by _WordStar_.
  This mounts its parent directory in _DOSBox-X_.
- Path filters: `reverse_slashes` uses `sed` again,
  to replace repeated slashes.
  The other filters remove use of both `cat` and `perl`.

## Version 0.3.0

- Use _DOSBox-X_ config file included in Sawyer's _WordStar_ archive,
  and apply changes with command-line options.
- Put _DOSBox-X_ options in _BASH_ array.
- Defineing alternate behaviours via the _DOSBox-X_ options array
  allows `DOSBox-X` to be invoked at a single location in the script.

## Version 0.2.0

- Improved option parsing. Despite what the help text says,
  there is no longer a discernment between 'Options' and 'Actions'.
- Path filters no longer use `sed`, which is replaced by
  `cat`, `tr`, and `perl`.

## Version 0.1.0

- Initial working version.
