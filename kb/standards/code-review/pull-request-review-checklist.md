---
id: std.code-review.pull-request-checklist
schema_version: 1
type: standard
status: draft
created: 2026-05-07
updated: 2026-05-07

title_vi: "Checklist review Pull Request"
title_en: "Pull Request review checklist"

tags:
  - code-review
  - pull-request
  - checklist
aliases:
  - pr checklist
  - review checklist
related: []
---

## Vietnamese

### TL;DR

- Ưu tiên review **logic/edge cases/rủi ro** trước; style đứng sau.
- PR cần mô tả rõ: **mục tiêu**, **phạm vi**, **rủi ro**, **cách test**, **kế hoạch rollout/rollback**.
- Chỉ approve khi thay đổi **đúng**, **test đủ**, và **đọc/maintain được**.

### Context/Why

- Code review giúp giảm bug, chia sẻ kiến thức, và giữ chất lượng/consistency lâu dài.

### Guidance

**1) Hiểu đúng mục tiêu & phạm vi**
- PR có nêu rõ *problem statement* và “done criteria” không?
- Phạm vi có “phình” không (scope creep)? Có tách PR được không?

**2) Correctness & edge cases**
- Xử lý lỗi rõ ràng (error paths), thông điệp lỗi hữu ích.
- Input validation hợp lý; tránh assumptions ngầm.
- Với code concurrent/async: race conditions, retries, idempotency.

**3) Tests**
- Có test cho đường đi chính và edge cases quan trọng.
- Test fail phải dễ debug (assert rõ, setup gọn).
- Nếu sửa bug: ưu tiên có test “repro” trước/sau.

**4) Security & secrets**
- Không log/commit secrets.
- Kiểm tra authn/authz (đúng quyền), injection (SQL/command), deserialization, SSRF (tuỳ bối cảnh).

**5) Performance & reliability**
- Tránh N+1 queries, vòng lặp tốn kém, IO blocking.
- Với thay đổi “hot path”: cân nhắc benchmark hoặc số liệu.

**6) Observability & operability**
- Logging đủ ngữ cảnh (request id/correlation id nếu có), không “spam”.
- Thêm metrics/alerts khi thay đổi ảnh hưởng vận hành.

**7) API/DB changes & rollout**
- Nếu có migration: tương thích ngược, thứ tự deploy an toàn.
- Có kế hoạch rollout (feature flag/canary) và rollback rõ.

### Examples

**PR description tốt (mẫu ngắn):**
- Mục tiêu: …
- Thay đổi chính: …
- Rủi ro: …
- Cách test: …
- Rollout/Rollback: …

**PR description kém:**
- “Fix bug” (không nói bug gì, test thế nào, rủi ro ra sao).

### Pitfalls

- Sa đà vào “nit” về formatting, bỏ qua logic/rủi ro.
- Approve khi PR không có context hoặc không có cách test.
- “Checklist tick-box”: tick cho đủ nhưng không đọc kỹ edge cases.

### References

- (Optional) Link tới tiêu chuẩn nội bộ hoặc guide về testing/security.

---

## English

### TL;DR

- Review **logic/edge cases/risk** first; style comes later.
- A PR should clearly state: **goal**, **scope**, **risk**, **how to test**, **rollout/rollback**.
- Only approve when the change is **correct**, **well-tested**, and **maintainable**.

### Context/Why

- Code review reduces bugs, spreads knowledge, and keeps quality/consistency over time.

### Guidance

**1) Confirm goal & scope**
- Does the PR include a clear problem statement and “done criteria”?
- Is scope creeping? Can it be split?

**2) Correctness & edge cases**
- Clear error handling (error paths) and useful error messages.
- Reasonable input validation; avoid hidden assumptions.
- For concurrent/async code: race conditions, retries, idempotency.

**3) Tests**
- Tests cover the happy path and key edge cases.
- Tests are debuggable (clear assertions, minimal setup).
- For bug fixes: prefer a repro test that fails before and passes after.

**4) Security & secrets**
- No secrets in logs or commits.
- Check authn/authz, injection risks (SQL/command), unsafe deserialization, SSRF (context-dependent).

**5) Performance & reliability**
- Avoid N+1 queries, expensive loops, blocking IO.
- For hot paths: consider benchmarks or supporting numbers.

**6) Observability & operability**
- Logs include enough context (request/correlation id if available) without spamming.
- Add metrics/alerts when operational behavior changes.

**7) API/DB changes & rollout**
- If migrations exist: backward compatibility and safe deploy order.
- Clear rollout plan (feature flags/canary) and rollback steps.

### Examples

**Good PR description (short template):**
- Goal: …
- Key changes: …
- Risks: …
- How to test: …
- Rollout/Rollback: …

**Bad PR description:**
- “Fix bug” (no context, no testing, no risk assessment).

### Pitfalls

- Nitpicking formatting while missing logic/risk.
- Approving without context or test instructions.
- Treating the checklist as box-ticking instead of actual review.

### References

- (Optional) Link to internal standards or testing/security guides.
