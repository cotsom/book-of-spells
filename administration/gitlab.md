---
description: Gitlab hints
---

# Gitlab

### Restore hashed repositories from backup

{% embed url="https://gitlab.com/gitlab-org/gitlab/-/issues/246567" %}

```bash
mkdir gitlab-backup
tar -C gitlab-backup/ -x -f 1605741345_2020_11_19_13.5.3_gitlab_backup.tar
cd gitlab-backup/repositories/@hashed/2c/62/
git clone 2c624232cdd221771294dfbb310aca000a0df6ac8b66b696d90ef06fdefb64a3.bundle repo/
git clone 2c624232cdd221771294dfbb310aca000a0df6ac8b66b696d90ef06fdefb64a3.wiki.bundle wiki-repo/
```
