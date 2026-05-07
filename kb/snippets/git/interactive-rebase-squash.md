---
id: snp.git.interactive-rebase-squash
schema_version: 1
type: snippet
status: stable
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
  - interactive rebase
related:
  - std.code-review.pull-request-checklist
---

## Vietnamese

### TL;DR

- Dùng `git rebase -i` để gộp (squash/fixup) commits trước khi merge.
- Nếu chỉ cần chỉnh vài commits gần nhất: dùng `git rebase -i HEAD~N`.
- Sau khi rewrite history, push bằng `--force-with-lease` (không dùng `--force` nếu không cần).

### Context/Why

- Lịch sử commit gọn giúp review dễ hơn và `git bisect` hữu ích hơn.

### Guidance

```text
# 0) Đảm bảo working tree sạch (commit hoặc stash thay đổi)
git status

# 1) Cập nhật refs từ remote
git fetch origin

# 2A) Chỉnh N commits gần nhất trên nhánh hiện tại
# (ví dụ: HEAD~3 để chỉnh 3 commits gần nhất)
git rebase -i HEAD~N

# 2B) Hoặc: chỉnh toàn bộ commits kể từ khi tách nhánh khỏi main
# (đổi origin/main nếu repo bạn dùng branch khác)
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

- Tip: Nếu hay tạo commit “fix lint”, “fix typo”… hãy dùng `git commit --fixup <sha>` rồi `git rebase -i --autosquash <base>` để gộp tự động.

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
- Nếu nhánh có merge commits: cân nhắc `git rebase -i --rebase-merges <base>` (chỉ dùng khi bạn hiểu rõ lịch sử sẽ thay đổi thế nào).

### References

- https://git-scm.com/docs/git-rebase
- https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History

---

## English

### TL;DR

- Use `git rebase -i` to squash/fixup commits before merging.
- If you only need to edit the last few commits: use `git rebase -i HEAD~N`.
- After rewriting history, push with `--force-with-lease` (avoid plain `--force` unless necessary).

### Context/Why

- A clean commit history makes reviews and `git bisect` more effective.

### Guidance

```text
# 0) Ensure a clean working tree (commit or stash changes)
git status

# 1) Update remote refs
git fetch origin

# 2A) Edit the last N commits on the current branch
# (e.g., HEAD~3 to edit the last 3 commits)
git rebase -i HEAD~N

# 2B) Or: edit all commits since the branch diverged from main
# (adjust origin/main as needed)
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

- Tip: If you often create small “fix” commits, use `git commit --fixup <sha>` + `git rebase -i --autosquash <base>` to squash them automatically.

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
- If your branch contains merge commits: consider `git rebase -i --rebase-merges <base>` (only if you understand how it reshapes history).

### References

- https://git-scm.com/docs/git-rebase
- https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History
