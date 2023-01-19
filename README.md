# gh-action-retry

A simple retry loop for bash in GitHub actions.

## Usage tl;dr

```yaml
uses: klothoplatform/gh-action-retry@v1
with:
  script: |
    echo "Some script that may intermittently fail. For example:"
    exit "$(( $(date +%s) % 3 ))"  # exit with a random code from 0 to 2
```

## Options

| name                | required? | default         | description                                                             |
|---------------------|-----------|-----------------|-------------------------------------------------------------------------|
| `script`            | yes       |                 | the bash script to run                                                  |
| `max-attempts`      | no        | 5               | how many attempts before the step exits out with failure                |
| `sleep-seconds`     | no        | 0               | how many seconds to wait between attempts                               |
| `description`       | no        | "Script"        | used to identify the step in the GitHub error, if all the attempts fail |
| `working-directory` | no        | `.`             | working directory for the script                                        |
| `bash-options`      | no        | `-euo pipefail` | `set` options to use while executing the script <sup>⚠️</sup>            |

<sup>
  <!-- markdown doesn't work within a sup :-( -->
  ⚠️ : <code>bash-options</code> are <em>not</em> sanitized, so if you provide this input, use a hard-coded value or a highly-trusted source.
  (Needless to say, the same applies for the <code>script</code> itself.)
</sup>
