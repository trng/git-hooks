#!/bin/sh

################################################################################
#
#
# VERSION NUMBERING CONTROL
#
#
# Auto increment patch|build number in pre-commit. (1.0.3 - major.minor.patch)
# "Smart behavior": version from this commit is compared to version from previous commit (HEAD^).
# If major.minor part is different in this commit and in previous commit - then patch number not incremented.
# And vice versa.
#
# The meaning of this behavior:
# If major.minor part changed (manually), then patch numbering restarted from zero (manually).
# No need to increment it in this commit.
#
# Example
#
# this commit: 1.1.0
# prev commit: 1.0.12
# Patch number (0) will not be incremented because 1.1 != 1.0
#
# this commit: 1.0.12
# prev commit: 1.0.12
# Patch number (12) will be incremented because 1.0 == 1.0
#
# Version number should be stored in ${SCRIPT_FNAME} file with this format:
#
#   #!/bin/bash
#   SCRIPT_VERSION=0.3.2
#
# TODO: validate version number structure for majorminorcurrent majorminorprevious.
################################################################################

SCRIPT_FNAME='github-push-and-merge'
CHANGED=$(git diff --name-only --cached --diff-filter=ACMR | grep -c -F "${SCRIPT_FNAME}")
if  [ "$CHANGED" -ne "0" ]; then
    echo ${SCRIPT_FNAME} changed and added to commit
    get_current_ver=`grep -m 1 "^SCRIPT_VERSION=" ${SCRIPT_FNAME}`
    vertemp=${get_current_ver#*=}
    majorminorcurrent=${vertemp%.*}
    get_previous_ver=`git show HEAD^:./github-push-and-merge | grep -m 1 "^SCRIPT_VERSION="`
    vertemp=${get_previous_ver#*=}
    majorminorprevious=${vertemp%.*}
    if [ ${majorminorcurrent} = ${majorminorprevious} ]; then
        echo "major.minor version is not changed. Patch number will be increased."
        awk -i inplace -vFS=. -vOFS=. '/^SCRIPT_VERSION=/{$3=($3+1)}1' ${SCRIPT_FNAME}
    fi
    git add ${SCRIPT_FNAME}
fi
