

## 🧪 Legacy Prototype: CherryPy + Selenium

### ➡️ Evolving into: **Box + S3 Pattern (V2.5)**

---

### 👀 What CherryPy + Selenium Typically Implied

| Tool         | Use in Context                                                                  |
| ------------ | ------------------------------------------------------------------------------- |
| **CherryPy** | Lightweight Python server used to serve previews or REST APIs during R\&D       |
| **Selenium** | Automated browser login/fetching from SharePoint/Box UIs that lacked API access |

---

### 🎯 Why It Was Used

| Use Case                         | Reason                                                                 |
| -------------------------------- | ---------------------------------------------------------------------- |
| 🔐 **Bypass lack of API access** | If SharePoint or Box OAuth wasn’t available, Selenium scraped UI       |
| 🧪 **Quick testing**             | CherryPy served as a fast local preview server for showing JSON > HTML |
| 🖥️ **Manual workflows**         | Browser-based preview interactions were easier to prototype            |
| 🌍 **No cloud setup**            | Could run entirely on a laptop or VM with no AWS setup required        |

---

### ⚠️ Risks and Limitations (That V2.5 Eliminates)

| Limitation              | Problem                                                       |
| ----------------------- | ------------------------------------------------------------- |
| 🚧 **Fragile**          | UI scraping breaks when Box/SharePoint DOM changes            |
| 🛡️ **Security risk**   | Browser automation may expose plaintext credentials           |
| 📉 **Unscalable**       | Selenium can't handle multi-user or async workflows           |
| 🧰 **Not cloud-native** | CherryPy lacks API Gateway, logging, scaling, or IAM control  |
| 📁 **Disk dependency**  | Downloads were stored locally, not versioned or secured in S3 |

---

### ✅ When CherryPy + Selenium *Still* Makes Sense (Early R\&D)

Use only when:

* 🔐 API access is **not available** and you need proof-of-concept scraping
* 💻 Running **offline or air-gapped** for demo/testing
* 👩‍🏫 Teaching or simulating end-user workflows in a classroom context

---

### 🔁 How to Modernize Into the **Box + S3 Pattern (V2.5)**

| Old                  | Replace With                                                 |
| -------------------- | ------------------------------------------------------------ |
| **CherryPy**         | → **Flask**, **API Gateway**, or **Streamlit**               |
| **Selenium**         | → **Box API + App Token** with scoped secure access          |
| **Manual downloads** | → **In-memory parse + direct Bedrock embedding**             |
| **Local UI**         | → **Cloud UI via Streamlit or React**                        |
| **No logging**       | → **S3-stored JSON logs** with version and reviewer metadata |

---

### 🧠 Final Thought

CherryPy + Selenium were excellent for fast prototyping, but they **do not meet audit, security, or scale requirements**.

For a modern, auditable system:

* ✅ Use **Box App Token + Webhook**
* ✅ Trigger a **Flask or Lambda-powered DSPy pipeline**
* ✅ Store embeddings in **S3 Vector Search**
* ✅ Serve previews via **Streamlit or lightweight viewer**
* ✅ Log reviewer edits and scoring to **S3 or DynamoDB**


