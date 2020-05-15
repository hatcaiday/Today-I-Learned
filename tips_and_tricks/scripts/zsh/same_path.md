## HOW TO KEEP SAME PATH FOLDER WHEN OPEN NEW TERMINAL

Add this code to .zshrc file

```
#Keep same path folder when open new terminal
# emulate bash PROMPT_COMMAND (only for zsh)
precmd() { eval "$PROMPT_COMMAND" }
# open new terminal in same dir
PROMPT_COMMAND='pwd > "${HOME}/.cwd"'
[[ -f "${HOME}/.cwd" ]] && cd "$(< ${HOME}/.cwd)"
```
