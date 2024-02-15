Auto increment patch (build) number using pre-commit hook.

Useful for preventing a commit with exactly the same version of the source code.

Version declaration must be in the following format:

         1.2.345 (major.minor.patch)



## ver1

Conditional increment depending on major.minor part changes (see comment inside script).

## ver2

Unconditional increment with every commit. Another version string splitter.

## ver3

Unconditional increment with every commit. Another (third) version string splitter.
