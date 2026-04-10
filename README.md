# Hated - Hater

## Clone repo command

Use this command to let code be checked before commit

```sh
git clone https://github.com/wilcorg/hated-hater.git && \
cd hated-hater && \
cat > .git/hooks/pre-commit <<'EOF'
#!/usr/bin/env sh
set -e

STAGED_PYTHON_FILES=".git/.staged-python-files"
git diff --cached --name-only --diff-filter=ACMR -z -- '*.py' '*.pyi' '*.ipynb' > "$STAGED_PYTHON_FILES"

if [ -s "$STAGED_PYTHON_FILES" ]; then
  xargs -0 uv run ruff check --fix < "$STAGED_PYTHON_FILES"
  xargs -0 uv run ruff format < "$STAGED_PYTHON_FILES"
  xargs -0 git add -- < "$STAGED_PYTHON_FILES"
fi

rm -f "$STAGED_PYTHON_FILES"
EOF
chmod +x .git/hooks/pre-commit
```

Use `git commit --amend --no-edit` to include changes into the last commit
