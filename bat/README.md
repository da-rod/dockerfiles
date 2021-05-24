# bat

A Docker image for bat (a cat(1) clone with wings) from https://github.com/sharkdp/bat.

## Why?

1. I like the tool
2. I am using a Ubuntu 20.04 instance and:
    1. (As of may 2021,) the version from `apt` is old (`0.12.1` vs `0.18.1`)
    2. The binary is available as `batcat` (because `bat` is provided by `bacula`)...
3. Since, I would need to make an alias for `bat`, why not having the latest version at least?!

## How?

Add the following function to your `.bashrc` (or whatever how you load your aliases and/or functions):

```bash
bat(){
        local BAT_THEME=Nord
        local DOCKER_IMG="peper/bat"
        local DOCKER_CMD="docker run -it --rm -e BAT_THEME=$BAT_THEME"
        for f in "$@"; do
        if [[ "$f" =~ ^\.\. ]]; then
                $DOCKER_CMD -v "$(cd "$(dirname "$f")" && pwd):/data" "$DOCKER_IMG" "$(basename "$f")"
        elif [[ "$f" =~ ^\/ ]]; then
                $DOCKER_CMD -v "$(dirname "$f"):/data" "$DOCKER_IMG" "$(basename "$f")"
        else
                $DOCKER_CMD -v "$PWD:/data" "$DOCKER_IMG" "$f"
        fi
done
}
```

Please refer to https://github.com/sharkdp/bat for its full documentation.
