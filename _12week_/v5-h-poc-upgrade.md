

## 🔄 Upgrade Plan: From CherryPy + Selenium Prototype → **Box + S3 Pattern (V2.5)**

---

### 🎯 Why Upgrade?

| CherryPy + Selenium Prototype           | Box + S3 Pattern (V2.5)                                                      |
| --------------------------------------- | ---------------------------------------------------------------------------- |
| Local preview server with basic routing | Cloud-deployed API using **Flask** or **Streamlit**                          |
| Web scraping of document portals        | Secure document access via **Box API + JWT App Token**                       |
| Manual download and disk-based parsing  | In-memory parsing + chunking, streamed directly into embedding               |
| Static local UI (preview only)          | Interactive **web UI** (Streamlit or React) with edit + feedback             |
| No traceability                         | Structured JSON logs stored in **S3** or **DynamoDB**                        |
| No versioning                           | Versioned logs with **reviewer ID**, **model version**, and rollback support |

---

### 🧱 Upgrade Architecture Overview

| Layer                 | V2.5 Target Implementation                                       |
| --------------------- | ---------------------------------------------------------------- |
| 🗂️ Document Source   | Replace Selenium with secure **Box API** and App Token auth      |
| 🧠 Embedding + Vector | Use **Bedrock** embeddings + **S3 Native Vector Search**         |
| 🔍 Reasoning Logic    | Integrate **DSPy Signature + Optimizer** per document type       |
| 📤 Output Delivery    | Serve structured previews via **Streamlit** or **Flask**         |
| 🔁 Logging + Feedback | Store editable previews and logs in **S3** or **lightweight DB** |

---

### ✅ Key Benefits of the Upgrade

| Area                   | Benefit                                                                          |
| ---------------------- | -------------------------------------------------------------------------------- |
| 🔐 **Security**        | Box App Token + scoped folder access replaces brittle browser scraping           |
| 📈 **Scalability**     | Stateless microservices for document fetch, embedding, and preview generation    |
| ✅ **Compliance**       | Audit-ready with versioned logs, reviewer IDs, model signatures                  |
| 💡 **UX Flexibility**  | Choose modern frontend (e.g., Streamlit, Flask+React) with async status handling |
| 🛠 **Maintainability** | Entire pipeline uses stable SDKs and managed services — no DOM scraping          |

---

### 📋 Phased Upgrade Checklist

| Phase          | Action                                                                            |
| -------------- | --------------------------------------------------------------------------------- |
| ✅ **Phase 0**  | Capture current prototype behavior (output formats, summaries, flags)             |
| 🔄 **Phase 1** | Replace Selenium with **Box SDK/API** integration for secure file fetch           |
| 📦 **Phase 2** | Convert CherryPy logic to **Flask app** or **Lambda function**                    |
| 🧠 **Phase 3** | Integrate **DSPy Signature + Optimizer**, scoped per document type                |
| 🖥 **Phase 4** | Build or enhance **Streamlit-based UI** for linking Box files and preview editing |
| 📝 **Phase 5** | Store previews + reviewer actions as versioned **JSON logs in S3**                |
| 🔔 **Phase 6** | (Optional) Add **Box Webhook** to auto-trigger pipeline on file upload            |

---

### 📎 Notes for Stakeholders

* 🔄 This is an **upgrade path**, not a full rewrite — key logic (e.g. prompt templates, flag types) can be reused and embedded in DSPy modules.
* ✅ Migrating from scraping to **Box + Bedrock** enables enterprise-grade scale, observability, and compliance.
* 💡 Preview UX remains intuitive and fast, now with support for **edit tracking**, **rerun support**, and **audit logging**.
* 📐 Aligns with **SR 11-7**, model governance standards, and internal control expectations for regulated document flows.





