# Title Case Converter

Since bash's parameter expansion includes case modification, there's no need for sed. Just a short function:

``` bash
tc() { set ${*,,} ; echo ${*^} ; }
```

Test (don't use quotes, since a title is typically no longer than a sentence, it shouldn't matter):

``` bash
tc FOO bar
```
Output:

`Foo Bar`

Fancy version that avoids capitalizing some conjunctions, articles and such:

``` bash
ftc() { set ${*,,} ; set ${*^} ; echo -n "$1 " ; shift 1 ; \
        for f in ${*} ; do \
            case $f in  A|The|Is|Of|And|Or|But|About|To|In|By) \
                    echo -n "${f,,} " ;; \
                 *) echo -n "$f " ;; \
            esac ; \
        done ; echo ; }
```

Test:

``` bash
ftc the last of the mohicans
```
Output:

The Last of the Mohicans 

Supposing the script's name is `ftc.sh`, then: `sed -i '1s#/sh$#/bash#' ftc.sh` should work.
