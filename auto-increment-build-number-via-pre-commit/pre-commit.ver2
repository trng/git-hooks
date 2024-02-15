#!/bin/sh

############################################################################################################
#
# VERSION NUMBERING CONTROL
#
#
# Auto increment patch (build) number using pre-commit hook.
#
#        1.2.345 (major.minor.patch)
#
#        Only patch number increments.
#        major.minor part stay unchanged.
#
#
# Version number should be stored in ${SCRIPT_FILE_NAME} file with one of these formats:
#
#
#        #!/usr/bin/env python
#        ...
#        SCRIPT_VERSION='1.2.345'
#        ...
#
#
#        #!/usr/bin/perl
#        ...
#        $script_version="1.2.345"
#        ...
#
#
#        #!/bin/bash
#        ...
#        SCRIPT_VERSION=1.2.345
#        ...
#
#
# Explanations:
#        - You can use quoted, doublequoted or unquoted string declaration - according to your programming language.
#        - Only first occurance of SCRIPT_VERSION will be changed! Because only one version declaration makes sense.
#        - Variable name with script version can be tuned in "MANDATORY VARIABLES" section below.
#        - File name should be placed in SCRIPT_FILE_NAME variable in "MANDATORY VARIABLES" section below
#
#
#
# DO NOT FORGET!
#
#        Typically, build (patch) number is reset to zero when major version is changed.
#        You should do it manually according to your practices.
#
#
# IMPORTANT!
#
#        Mandatory variables value should be set manually (see 'MANDATORY VARIABLES' section below).
#
############################################################################################################



##############################################
#         MANDATORY VARIABLES                #
##############################################

SCRIPT_FILE_NAME='svman'
VERSION_STRING_DECLARATION="^SCRIPT_VERSION="

##############################################
##############################################



CHANGED=$(git diff --name-only --cached --diff-filter=ACMR | grep -c -F "${SCRIPT_FILE_NAME}")
if  [ "$CHANGED" -ne "0" ]; then
    echo ${SCRIPT_FILE_NAME} changed and added to commit. "pre-commit" hook will be applied for increment build number.
    awk -i inplace -vFS=. -vOFS=. -vVSD=${VERSION_STRING_DECLARATION} '$0 ~ VSD{ str=gensub( /[^'"'"'"'']/, "", "g", $0) ; $3=($3+1) substr(str,1,1) }1' ${SCRIPT_FILE_NAME}
    git add ${SCRIPT_FILE_NAME}
fi
