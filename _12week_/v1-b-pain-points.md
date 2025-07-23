

## ⚠️ Pain Points – **Version 1 Architecture (Salesforce + SharePoint + DSPy + Bedrock + S3 Vector)**

---

### 🔗 **Integration & Data Flow Challenges**

| Pain Point                        | Why It Matters                                                                                                       |
| --------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| **🧩 SharePoint → AWS doc fetch** | Pulling files via Microsoft Graph API adds latency and authentication complexity (OAuth tokens, expired links, etc.) |
| **🧱 Fragmented pipeline**        | Orchestration spans Salesforce → Lambda → Bedrock → DSPy → S3 → back to Salesforce, increasing failure points        |
| **🌐 External embedding delay**   | Real-time preview may feel slow due to cold-starts in Lambda or ECS                                                  |
| **📎 Link-only upload**           | No native SharePoint file browser in Salesforce UI (unless custom-built or via MuleSoft connector)                   |

---

### 🧠 **Model Performance & LLM Behavior**

| Pain Point                      | Why It Matters                                                                                                               |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **🎯 Prompt inconsistency**     | DSPy needs good Signature and few-shot setup or you’ll get generic, hallucinated summaries                                   |
| **📏 Lack of scoring criteria** | Flagging “missing sections” requires structured standards — if this isn't well modeled in Salesforce, flagging logic weakens |
| **📚 Prompt token limits**      | Large docs or many chunks could exceed Bedrock model limits (esp. Claude v1.3 or Titan) unless chunked smartly               |
| **🔄 Embedding updates**        | If standards change or model improves, you must **re-index** old documents — S3 Vector doesn't yet support versioned indexes |

---

### 🔒 **Security & Governance Concerns**

| Pain Point                               | Why It Matters                                                                                                            |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **🔐 Cross-cloud compliance**            | Moving regulated docs from M365 → AWS might conflict with org data policies or risk team objections                       |
| **🚫 No RBAC in S3 Vector Search (yet)** | All embedding/query logic must enforce security from upstream; vector store itself doesn’t have per-user access control   |
| **🧾 Logging sensitive output**          | JSON previews stored in S3 or Salesforce must be encrypted, versioned, and auditable to meet SR 11-7 or SOC2 expectations |

---

### 🖥️ **User Experience Friction**

| Pain Point                      | Why It Matters                                                                                                                                |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **🧵 Lightning UI limitations** | Embedding a rich preview UI (e.g., collapsible flags, approve/edit workflows) may be clunky in Lightning without LWC custom work              |
| **⏳ Latency perception**        | Users may perceive the delay between upload and preview generation as broken unless there's status feedback                                   |
| **✏️ Edits not versioned**      | If a reviewer edits a preview summary, and it overwrites the original, you lose traceability unless versioned logs are implemented from day 1 |
| **❌ No retry path**             | If DSPy or Bedrock fails mid-pipeline, is there a user-visible retry option or error message? (Most Salesforce UIs won’t show it natively)    |

---

## 📌 Top 3 to Flag in Your Meetings

1. **🔗 Cross-platform complexity** — Too many hops: Salesforce → SharePoint → AWS → Salesforce → S3
2. **🧠 Weak grounding without a structured standards model** — The system can't "flag missing fields" unless it knows what’s expected for each document type
3. **🔒 Governance gap** — You’re crossing clouds with compliance-critical content. Legal and IT risk teams will care **a lot**.


