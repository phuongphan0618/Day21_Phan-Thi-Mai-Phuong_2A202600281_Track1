# AI Risk Framework — Research Paper Summarization MVP
## R1 — RULES
Mục tiêu:
- Giảm hallucination trong academic summaries
- Giữ trust với user research/student
- Protect customer queries + research workflow

---
### KHÔNG được làm
- Paste customer research queries, unpublished thesis drafts hoặc internal prompts
  vào ChatGPT public / Claude public
- Upload full licensed papers lên public AI tools nếu chưa verify usage rights
- Generate summaries không có citation/source traceable
- Deploy prompt hoặc retrieval pipeline mới trực tiếp lên production mà chưa review hallucination cases
- Trả lời technical claims vượt quá nội dung paper gốc

---
### Được làm (approved workflow)
- DÙNG OpenAI Enterprise / Claude for Work
  → data không train
  → approved cho internal usage
- DÙNG Semantic Scholar + arXiv APIs
  → chỉ retrieve metadata/public papers
- Nếu parsing quality thấp:
  → fallback về abstract-only summary
- Nếu confidence thấp:
  → show warning + source links thay vì generate thêm

---
### Hậu quả vi phạm
- Lần 1:
  Founder review workflow trực tiếp
- Lần 2:
  Remove production access / pause deployment permission

---
### Ai update rules?
Founder + tech lead

Update ngay khi:
- đổi model vendor
- có hallucination incident
- đổi API policy
- có legal/license concern mới

Không chờ quarterly review.

---

## R2 — RAILS
Mục tiêu:
- Prevent hallucination trước khi tới user
- Audit được mọi AI output
- Crisis xảy ra vẫn verify được trong vài phút

---
### Current Rails Stack

| Mục tiêu | Tool | Cost |
|---|---|---|
| Log mọi LLM request/response | Helicone | Free tier |
| Chặn API keys/secrets vào git | git-secrets + pre-commit hooks | $0 |
| Code review trước deploy | GitHub branch protection | $0 |
| Giảm inference cost | Redis/file summary cache | ~$10–20/tháng |
| Detect PDF parsing lỗi | Parsing quality threshold | Internal |
| Fallback nếu parse fail | Abstract-only fallback | Internal |
| Approved enterprise AI usage | OpenAI Enterprise / Claude for Work | Per-user |

---

### Priority setup order

#### Priority #1 — Must-have
- Helicone logging
- git-secrets
- Branch protection
- Citation-required prompting

#### Priority #2 — Reliability
- Summary caching
- Parsing quality detection
- Confidence threshold
- Abstract fallback

#### Priority #3 — Advanced
- LangFuse self-host
- Prompt regression tests
- Automatic hallucination evaluation

---
### Crisis response benefit

Nếu có incident kiểu:
“AI summary nói sai nội dung paper và bị tweet viral”

#### Verify nhanh
- Search Helicone logs
- Match exact prompt + response
- Check retrieval chain
- Verify screenshot thật/fake

#### Stop bleeding
- Tighten prompts
- Disable unsupported synthesis
- Force citation-only mode
- Rollback model/prompt version

#### Audit
- Check affected users
- Review parsing quality
- Identify hallucination pattern

Không có rails:
```
→ không biết AI đã nói gì
→ không reproduce được issue
→ founder phản ứng quá chậm
```
---
## R3 — RITUAL
Mục tiêu:
- Build habit kiểm tra hallucination sớm
- Giữ founder gần với research users thật
- Detect trust issues trước khi churn

---
| Ritual | Mô tả | Tần suất | Cost |
|---|---|---|---|
| **Friday 30' Risk Review** | Founder + tech lead review: hallucination cases, parsing failures, customer complaints, vendor/API changes, inference cost spikes | Mỗi tuần | 30' |
| **Customer Friday** | Founder call 1 student/research user: *"Summary nào làm bạn thấy thiếu trust?"* / *"Có paper nào AI hiểu sai không?"* | Mỗi tuần | 30' |
| **Onboarding AI Safety Chat** | Day 1: founder explain AI safety rules + workflow. Day 7: review prompts + citation requirements | Per hire | 30' |
| **Pre-launch Review** | Trước launch feature: 2 người review prompts, citations, edge cases, fallback UX, hallucination risks | Per feature | 30' |
| **Hallucination Review Session** | Team chọn random summaries mỗi tuần để kiểm tra factual accuracy + traceability | Mỗi tuần | 20' |
| **Incident War Game** | Simulate incident: *"AI summary hiểu sai paper nổi tiếng và tweet viral 100K views"* | Quarterly | 60' |


