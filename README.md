# Hated - Hater

## Clone repo command

Use this command to let code be checked before commit

```sh
git clone https://github.com/wilcorg/hated-hater.git && \
cd hated-hater && \
cat > .git/hooks/pre-commit <<'EOF'
#!/usr/bin/env sh
set -e
uv run ruff check .
uv run ruff format --check .
EOF
chmod +x .git/hooks/pre-commit
```

Use `git commit --amend --no-edit` to include changes into the last commit
