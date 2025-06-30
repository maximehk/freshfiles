## Sample use-case in bash

```shell
# `./update_files.sh` is invoked if any of these files are missing or more than 1 hour old
freshfiles --max-age-seconds 3600 file1 file2 || ./update_files.sh



freshfiles --max-age-seconds 3600 .authfile && echo "no auth needed" || { 
    echo "authenticating" # replace with actual authentication
    touch .authfile
}


```


## Using justfiles

Project link: https://just.systems/man/en/introduction.html

```
[private]
_maybe_authenticate:
  #!/usr/bin/env bash
  set -euo pipefail
  freshfiles --max-age-seconds 3 .authfile && echo "auth still valid" || { 
        echo "authenticating" # replace with actual authentication
        touch .authfile
  }

run: _maybe_authenticate
  @echo "... do work with valid auth"
```