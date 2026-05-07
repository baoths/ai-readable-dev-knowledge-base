---
id: snp.git.interactive-rebase-squash
schema_version: 1
type: snippet
status: draft
created: 2026-05-07
updated: 2026-05-07

title_vi: "Squash commits bằng interactive rebase"
title_en: "Squash commits with interactive rebase"

tags:
  - git
  - history
  - rebase
aliases:
  - squash commits
  - git squash
related: []
---

## Vietnamese

### TL;DR

- Dùng `git rebase -i` để gộp (squash/fixup) commits trước khi merge.
- Sau khi rewrite history, push bằng `--force-with-lease` (không dùng `--force` nếu không cần).

### Context/Why

- Lịch sử commit gọn giúp review dễ hơn và `git bisect` hữu ích hơn.

### Guidance

```text
# 1) Cập nhật refs từ remote
git fetch origin

# 2) Rebase tương tác lên base branch (đổi origin/main nếu repo bạn dùng khác)
git rebase -i origin/main

# 3) Trong editor:
# - giữ commit đầu là "pick"
# - đổi các commit muốn gộp thành "s" (squash) hoặc "f" (fixup)
# - lưu và thoát

# 4) Nếu có conflict: resolve rồi
git rebase --continue

# 5) Chạy test (tuỳ dự án)
# 6) Push lại nhánh đã rewrite
git push --force-with-lease
```

### Examples

Ví dụ file todo khi rebase:

```text
pick a1b2c3d Add API endpoint
fixup d4e5f6g Fix lint
squash h7i8j9k Add tests
```

### Pitfalls

- **Không** rewrite history trên nhánh đang được nhiều người dùng chung.
- PR đang review có thể bị “mất context” nếu rewrite quá nhiều lần.
- Luôn ưu tiên `git push --force-with-lease` để tránh ghi đè nhầm thay đổi của người khác.

### References

- https://git-scm.com/docs/git-rebase
- https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History

---

## English

### TL;DR

- Use `git rebase -i` to squash/fixup commits before merging.
- After rewriting history, push with `--force-with-lease` (avoid plain `--force` unless necessary).

### Context/Why

- A clean commit history makes reviews and `git bisect` more effective.

### Guidance

```text
# 1) Update remote refs
git fetch origin

# 2) Interactive rebase onto the base branch (adjust origin/main as needed)
git rebase -i origin/main

# 3) In the editor:
# - keep the first commit as "pick"
# - change commits to "s" (squash) or "f" (fixup)
# - save and exit

# 4) If conflicts happen: resolve, then
git rebase --continue

# 5) Run your tests (project-specific)
# 6) Push rewritten branch
git push --force-with-lease
```

### Examples

Example rebase todo:

```text
pick a1b2c3d Add API endpoint
fixup d4e5f6g Fix lint
squash h7i8j9k Add tests
```

### Pitfalls

- Do **not** rewrite history on shared branches used by other people.
- Excessive rewrites can make PR review conversations harder to follow.
- Prefer `--force-with-lease` to avoid accidentally overwriting someone else’s updates.

### References

- https://git-scm.com/docs/git-rebase
- https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History
