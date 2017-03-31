## Bash urlencode

```bash
urlencode() {
  # urlencode <string>

  local LANG=C
  local length="${#1}"
  for (( i = 0; i < length; i++ )); do
    local c="${1:i:1}"
    case $c in
      [a-zA-Z0-9.~_-]) printf "$c" ;;
      *) printf '%%%02X' "'$c" ;;
    esac
  done
}
```

Reference: https://gist.github.com/cdown/1163649
