# Git

## Advanced

Pushing to multiple Git repos

```bash
# Add Git repo as cake
git remote add cake git@ssh.dev.azure.com:v3/Potato
# Register repo as push url
git remote set-url --add --push cake git@ssh.dev.azure.com:v3/Potato
# Add next git
git remote set-url --add --push cake git@github.com:Potato.git
# Push to both
git push cake
```

__Please note that you cannot pull from multiple repos!!!__
