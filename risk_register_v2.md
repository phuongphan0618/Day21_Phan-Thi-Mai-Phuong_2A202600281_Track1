# risk_register_v2.md

# TOP 10 RISKS — Research Paper Summarization Startup

Context:
- 5-person AI startup
- Seed-stage mindset
- Runway assumption: ~12–24 months
- Core dependency: retrieval + summarization + trust

---

# RISK 1: LLM Pricing Spike

- Type: Vendor

- If:
DeepSeek/OpenAI tăng pricing hoặc giảm free/cheap inference tier sau khi user volume tăng,

- Then:
summary generation cost tăng đột ngột, forcing startup phải limit usage hoặc degrade UX,

- Leading to:
~4 tháng runway mất do burn rate tăng nhanh hơn planned.

- Likelihood (1-5):
4
(Vendor pricing changes xảy ra thường xuyên trong AI market hiện tại)

- Impact (1-5):
4

- Mitigation:
1. Cache summaries aggressively
2. Prepare secondary cheaper model fallback
3. Add usage/rate limits theo user tier

---

# RISK 2: Vendor Rate Limit Lock

- Type: Vendor

- If:
LLM provider sudden rate-limit traffic trong peak hours hoặc exam/research season,

- Then:
users không generate được summaries hoặc phải wait quá lâu,

- Leading to:
~3 tháng runway mất do retention drop từ early adopters.

- Likelihood (1-5):
4
(Seed startup không có enterprise priority access)

- Impact (1-5):
3

- Mitigation:
1. Queue + retry system
2. Precompute/cache popular papers
3. Multi-provider routing fallback

---

# RISK 3: Model ToS Change

- Type: Vendor

- If:
Vendor update ToS liên quan academic/research summarization hoặc content storage,

- Then:
startup phải disable/rebuild một phần workflow rất nhanh,

- Leading to:
~3 tháng runway mất do engineering rewrite + service interruption.

- Likelihood (1-5):
3

- Impact (1-5):
3

- Mitigation:
1. Avoid vendor lock-in
2. Keep prompts/model layer abstracted
3. Maintain local fallback pipeline cho abstract summaries

---

# RISK 4: Technical Hallucination

- Type: Customer-facing

- If:
AI summary hiểu sai technical claim hoặc fabricate limitation/conclusion của paper,

- Then:
research users mất trust và quay lại manual reading workflow,

- Leading to:
~4 tháng runway mất do churn + failed word-of-mouth adoption.

- Likelihood (1-5):
4
(Summarization của technical papers inherently high-risk)

- Impact (1-5):
4

- Mitigation:
1. Citation-required summaries
2. Confidence threshold + fallback mode
3. Weekly hallucination review sessions

---

# RISK 5: Wrong Paper Ranking

- Type: Customer-facing

- If:
relevance ranking retrieve nhiều low-quality hoặc irrelevant papers cho user query,

- Then:
user không tìm được “first useful paper” trong vài phút đầu,

- Leading to:
~2 tháng runway mất do onboarding failure + low retention.

- Likelihood (1-5):
4

- Impact (1-5):
2

- Mitigation:
1. Lightweight reranking layer
2. User feedback loop (accept/reject)
3. Quality filtering theo citation/relevance threshold

---

# RISK 6: PDF Parsing Collapse

- Type: Customer-facing

- If:
PDF parser fail trên papers có equations/tables/2-column formatting,

- Then:
AI summary generate từ corrupted text hoặc missing sections,

- Leading to:
~3 tháng runway mất do silent accuracy degradation.

- Likelihood (1-5):
4

- Impact (1-5):
3

- Mitigation:
1. Parsing quality score
2. Abstract-only fallback
3. Manual validation dataset cho parsing edge cases

---

# RISK 7: Founder Bottleneck

- Type: Founder-bandwidth

- If:
Founder/main engineer bận thesis/interview/sick vài ngày đúng lúc retrieval pipeline fail,

- Then:
critical production issue không được fix nhanh,

- Leading to:
~2 tháng runway mất do stalled iteration + frustrated early users.

- Likelihood (1-5):
3

- Impact (1-5):
2

- Mitigation:
1. Document deploy/debug flow
2. Monitoring + alerts
3. Reduce MVP scope aggressively

---

# RISK 8: GDPR / Data Retention Issue

- Type: Regulatory

- If:
startup log hoặc store user queries/research topics mà không disclosure rõ,

- Then:
có risk compliance issue với GDPR hoặc university data policies,

- Leading to:
~3 tháng runway mất do legal cleanup + forced infra changes.

- Likelihood (1-5):
2

- Impact (1-5):
3

- Mitigation:
1. Minimize stored user data
2. Add transparent privacy notice
3. Auto-delete old logs after fixed period

---

# RISK 9: Copyright / License Violation

- Type: Regulatory

- If:
startup accidentally cache hoặc redistribute licensed paper content beyond allowed usage,

- Then:
publisher takedown request hoặc legal escalation xảy ra,

- Leading to:
~5 tháng runway mất do legal + forced architecture rewrite.

- Likelihood (1-5):
3

- Impact (1-5):
4

- Mitigation:
1. Store metadata + snippets only
2. Link back to original source
3. License review checklist trước caching full text

---

# RISK 10: Cross-paper Synthesis Failure

- Type: Customer-facing

- If:
future “Cross Paper Synthesizer” combine multiple papers sai logic hoặc invent consensus không tồn tại,

- Then:
users distrust toàn bộ platform vì output nghe convincing nhưng technically wrong,

- Leading to:
~6 tháng runway mất do catastrophic trust collapse.

- Likelihood (1-5):
3

- Impact (1-5):
5

- Mitigation:
1. Delay feature until retrieval quality stable
2. Force source traceability per claim
3. Human-eval benchmark trước public launch

---

# KILL ZONE RISKS

| Risk | Score | Why dangerous |
|---|---:|---|
| LLM Pricing Spike | 16 | Burn rate explode silently |
| Technical Hallucination | 16 | Core trust collapse |
| PDF Parsing Collapse | 12 | Silent corruption risk |
| Cross-paper Synthesis Failure | 15 | “Confidently wrong” AI destroys credibility |

---

