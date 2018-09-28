## colorwdiff

### Usage:

    diff file1 file2 | colorwdiff [option(s)]
    diff -U 3 file1 file2 | colorwdiff
    diff file1 file2 | colorwdiff | less -R

colorwdiff was invented as an alternative to colordiff and wdiff/cwdiff.  There are some little quirks about wdiff which did not flow well for my applications.  For one, the way if a segment flagged for removal is at the beginning of a line, it is split off in its own line with the remainder of the text printing 2 lines after it.  Also, I did not want to break the entire file up into words, then diff it that way, as with this approach there is a loss of the logical grouping of the lines and the resulting output often seems disjointed and confusing in the context of line output.  So my approach is to first diff the lines as diff would normally, break _these_ results into words, then diff the words in order to show which words have been changed within the lines (follow that?)

The result is an output that appears _exactly as diff output_, except colorizing only the text which has changed, rather than the entire line as colordiff does.  This makes spotting the changes within the lines quite easy.

As I mainly needed it for comparing HTML files, I also desired to be able to treat HTML tags autonomously, even if they are adjacent to words or other tags.

### Options:

    -nc         do not colorize, only show [--], {++} wrappers
    -w          retain [--], {++} wrappers when colorizing
    -word       break at word boundaries (default breaks at \\s\\S, \\S\\s boundaries)
    -nohtml     don't treat html tags autonomously (default does)
    -noarrows   suppress <, > flags when using normal diff (always prints file1|file2 divider in this case)
                (helpful when you want to copy and paste output)

colorwdiff uses wdiff's default remove/add container tags.  Unlike wdiff, there is no option to customize these.

colorwdiff with no args will print colored output with [--], {++} wrappers hidden, break words at space/non-space boundaries, retain html tags as a word, displayed in the same format as the input diff.

If the -nc option is passed, colorwdiff will not colorize, but will print the [--], {++} wrappers for post-processing such as formatting for HTML output.

Like wdiff, a default "word" is either a series of space characters, or a series of non-space characters.  Using the -word option will break "words" at word boundaries.

Apply options to diff for your application.

Unlike wdiff/cwdiff, which can be used as a wrapper for diff, colorwdiff is only used as a post-process treatment of diff output.  It will accept "normal" diff and unified diff outputs happily.  I have not experimented with the entire gambit of diff options to see what the effect will be on colorwdiff.

### Bugs

Only a one or two innocuous ones (that I have seen) which I can't think of right now :-)
