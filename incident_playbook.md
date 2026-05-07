# Tình huống

9h30 sáng.

Một customer tweet screenshot:
> “AI summary của startup này hiểu sai nội dung paper.”

200 retweets trong 30 phút.
Có signal bắt đầu viral.

---
# Bước 1 — VERIFY (0–5 phút)

## Check logs ở đâu?

### 1. Helicone logs
URL:
https://www.helicone.ai/dashboard

Check:

* timestamp
* user/session ID
* prompt
* retrieved context
* full model response

---
### 2. Retrieval logs / database

Check:

* paper ID
* arXiv/Semantic Scholar source
* parsing quality score
* citation mapping

Questions:

* Có retrieve sai paper không?
* Parse PDF có fail không?
* Citation chain có missing không?

---
## Verify thật hay fake như nào?

So sánh:

* timestamp screenshot
* exact wording
* response formatting
* user/session ID

Nếu:

* không có log match
* wording khác production
* timestamp không tồn tại

→ có khả năng screenshot fake/edit.

---
# Bước 2 — STOP THE BLEEDING (5–15 phút)

## Chọn option: TIGHTEN PROMPT + SOFT KILL

---
## Action thực hiện ngay

### Tighten prompt

* Force citation-required summaries
* Không cho generate unsupported claims
* Giảm free-form synthesis

### Soft kill fallback

Nếu parsing quality thấp:
→ chỉ show:

* abstract
* metadata
* citation/source links

Không generate AI summary mới.

---
## Vì sao không hard kill?

Core value của product là:

* retrieval
* paper discovery

Nếu hard shutdown:

* toàn bộ user bị ảnh hưởng
* trust giảm mạnh hơn

Problem hiện tại là:

* summary quality
* không phải infra/security breach

---
## Deploy ngay

* rollback prompt version
* enable low-confidence mode
* disable unsupported synthesis
* cache known-good summaries

---
# Bước 3 — Customer Communication (15–25 phút)

Hi [Customer],

This is [Founder] — I personally reviewed the issue with our AI this morning.

What happened:
Our AI generated an incorrect summary about a paper in your session. That response was wrong.

What I’m doing:

* Tightened citation requirements immediately
* Disabled unsupported free-form summaries temporarily
* Reviewing retrieval + parsing logs personally

Making it right:
I’m refunding your subscription/research credits today — no forms needed.

I’d also appreciate the original query or screenshot context if you’re open to sharing it. It’ll help me reproduce and fix the issue faster.

I’ll follow up again within 24 hours with a clearer root-cause update.

— [Founder Name]
[[founder@company.com](mailto:founder@company.com)]

---
# Bước 4 — Public Response (25–30 phút)

Hi everyone — I’m [Founder]. I just reviewed the paper-summary issue reported this morning.

I’ve tightened citation rules and temporarily reduced unsupported AI summaries while I investigate the root cause.

Reaching out to the affected user directly now. More updates within 24h.

---
# Follow-up Tasks (same day)

```
[ ] Add parsing quality scoring
[ ] Add confidence threshold UI
[ ] Add hallucination evaluation checks
[ ] Improve citation traceability
[ ] Cache validated summaries
[ ] Add rollback shortcut cho prompt versions
```
