# Current Runway
- Estimated runway: >= 24 months
- Impact được đo bằng số tháng runway có thể mất sau incident

---

## Bước 1

| Risk Type | Mô tả  | Áp dụng cho startup |
|---|---|---|
| **Vendor Risk** | DeepSeek/OpenAI thay đổi pricing, rate limit hoặc API policy khiến summary generation chậm, fail hoặc quá đắt để scale | Cache summaries để giảm số lần gọi model. Fallback về abstract-only summary. Rate limiting + retry queue khi traffic cao |
| **Customer-facing AI Risk** | AI summary hallucinate hoặc hiểu sai technical content của paper khiến user mất trust | Force citation/source links. Hiển thị confidence warning nếu parse thấp. Cho user mở lại paper gốc nhanh. Fallback sang extractive/abstract summary thay vì generate tự do |
| **Founder-bandwidth Risk** | Founder/main engineer unavailable khi parsing/retrieval pipeline gặp critical bug | Logging + monitoring tự động. Automate fallback logic để giảm manual intervention |

---
## Bước 2

### 1. Vendor Risk
If DeepSeek/OpenAI thay đổi pricing, rate limit hoặc API policy đột ngột,

Then paper summarization trở nên chậm, fail hoặc quá đắt để scale trong giờ cao điểm,

Leading to inference cost tăng + user experience giảm = mất khoảng 4 tháng runway.

### 2. Customer-facing AI Risk
If AI summary hallucinate hoặc hiểu sai technical meaning của paper,

Then users mất trust vào summaries, phải đọc lại full paper hoặc share incident trên social media,

Leading to retention drop + churn từ early adopters = mất khoảng 3 tháng runway.

### 3. Founder-bandwidth Risk
If founder/main engineer unavailable vài ngày trong lúc parsing hoặc retrieval pipeline gặp critical bug,

Then production issue không được fix nhanh, summaries fail liên tục,

Leading to delayed MVP iteration + user frustration = mất khoảng 2 tháng runway.


## Bước 3

| Risk Type | Likelihood (1–5) | Impact (1–5) | Score | Quadrant |
|---|---:|---:|---:|---|
| **Vendor Risk** | 4 | 4 | 16 | KILL ZONE |
| **Customer-facing AI Risk** | 3 | 3 | 9 | WATCH / MITIGATE |
| **Founder-bandwidth Risk** | 3 | 2 | 6 | WATCH / MITIGATE |

## Bước 4

```
                    Likelihood
               Low (1-2)      High (4-5)

            ┌──────────────┬────────────────┐
 High       │              │ Vendor Risk    │
 (>3mo)     │              │ Score: 16      │
            │              │   KILL ZONE    │
Impact      ├──────────────┼────────────────┤
 Low        │ Founder      │ Customer-facing│
 (<3mo)     │ Risk         │ AI Risk        │
            │ Score: 6     │ Score: 9       │
            │    Watch     │    Mitigate    │
            └──────────────┴────────────────┘
```