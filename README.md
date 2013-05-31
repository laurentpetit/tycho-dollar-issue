# Description

This repository shows a minimalist of a Maven Tycho issue:

- As soon as one of the directories packaged in a bundle contains the dollar sign $ in its name, the preparation phase of tycho-surefire-plugin will fail.
- This occurs on my OSX X box, and has been reported to also occur on Linux box. Seems like Windows machines are not affected by the bug, which involves "chmod".

In this repo, there's a plugin named "core" which contains a lib/ directory with a directory containing an $.

This directory is included in the bundle when packaged as a jar.

# Reproduce the error

    git clone https://github.com/laurentpetit/tycho-dollar-issue
    cd tycho-dollar-issue
    mvn clean install

# Error report

    [INFO] --- tycho-surefire-plugin:0.18.0:test (default-test) @ test ---
    [WARNING] -------------------------------
    [WARNING] Standard error:
    [WARNING] -------------------------------
    [WARNING] 
    [WARNING] -------------------------------
    [WARNING] Standard output:
    [WARNING] -------------------------------
    [WARNING] /bin/sh: line 0: cd: /Users/laurentpetit/Documents/test/tycho-dollar-issue/test/target/work/plugins/core_0.0.1.201305312154/lib/foo: No such file or directory

    [WARNING] -------------------------------
    [INFO] ------------------------------------------------------------------------
    [INFO] Reactor Summary:
    [INFO] 
    [INFO] parent ............................................ SUCCESS [0.557s]
    [INFO] core .............................................. SUCCESS [1.243s]
    [INFO] test .............................................. FAILURE [5.548s]
    [INFO] core.feature ...................................... SKIPPED
    [INFO] updatesite ........................................ SKIPPED
    [INFO] aggregator ........................................ SKIPPED
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD FAILURE
    [INFO] ------------------------------------------------------------------------
    [INFO] Total time: 43.976s
    [INFO] Finished at: Fri May 31 23:54:47 CEST 2013
    [INFO] Final Memory: 36M/465M
    [INFO] ------------------------------------------------------------------------
    [ERROR] Failed to execute goal org.eclipse.tycho:tycho-surefire-plugin:0.18.0:test (default-test) on project test: Execution default-test of goal org.eclipse.tycho:tycho-surefire-plugin:0.18.0:test failed: Unable to unpack jar /Users/laurentpetit/Documents/test/tycho-dollar-issue/core/target/core-0.0.1-SNAPSHOT.jar: chmod exit code was: 1 -> [Help 1]
