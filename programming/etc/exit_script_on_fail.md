## Exit script on fail

If you want to let your script exit on fail, use `set -e`.

Example: test.sh
```bash
#!/bin/bash

set -e
./wrong_file_path.sh

echo "good!"
```

```
$ ./test.sh
./test.sh: line 5: ./wrong_file_path.sh: No such file or director
```

You can add callback function using `trab`

Example: test.sh
```bash
#!/bin/bash

set -e
function onFail {
  echo -e "Fail!"
}
trap onFail EXIT

./wrong_file_path.sh

echo "good!"
```

```
$ ./test.sh
./test.sh: line 9: ./wrong_file_path.sh: No such file or directory
Fail!
```

Reference:  
https://stackoverflow.com/questions/2870992/automatic-exit-from-bash-shell-script-on-error  
https://stackoverflow.com/questions/2129923/bash-run-command-before-a-script-exits
