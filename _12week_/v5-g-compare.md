

## 📊 Spec Sheet: **Box + S3 Pattern vs. Managed Pipeline Pattern**

| Feature Category            | 🔶 **Box + S3 Pattern (V2.5)**                                | ✅ **Managed Pipeline Pattern**                                                |
| --------------------------- | ------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| **Document Trigger**        | Manual trigger or UI-based file picker                        | **Box Webhook** auto-triggers via secure upload folder                        |
| **File Access Method**      | On-demand fetch using Box API and short-lived tokens          | **App token** with event-driven access, optional signed URLs                  |
| **Change Detection**        | None — all docs embedded on upload                            | **File hash check** before embedding → prevents redundant vectorization       |
| **LLM Integration**         | Bedrock Titan/Claude called directly per document             | **Lambda-invoked Bedrock** logic scoped to change events                      |
| **Vector Store**            | Amazon S3 Vector Search with manually managed namespace       | **S3 Vector + Metadata DB** fully managed and filtered by doc/session/version |
| **DSPy Signature Use**      | One signature per doc type, must be selected manually         | Signature auto-selected by doc type, tracked by version in logs               |
| **DSPy Optimizer Use**      | Optional, must be configured separately                       | Built-in scoring + feedback storage per preview session                       |
| **Logging / Versioning**    | JSON in S3; reviewer overwrites editable field                | **Preview + reviewer edits versioned in Postgres or DynamoDB**                |
| **Frontend UI**             | Streamlit or Flask/React tied to processor                    | **Viewer app decoupled** from processing pipeline (pulls from DB or API)      |
| **Preview Display**         | Blocking call; must wait for LLM response                     | **Asynchronous polling** with preview status (e.g. `IN_PROGRESS`, `DONE`)     |
| **UX Responsiveness**       | Slower with no feedback                                       | Includes **progress bars, rerun buttons, retry notices**                      |
| **Retry Handling**          | Manual reupload or script rerun                               | Automatic retry queue + visibility in UI                                      |
| **Reviewer Feedback**       | Not structured or tracked                                     | **Structured audit notes stored per doc + reviewer + version**                |
| **Rollback Support**        | Overwrites prior runs                                         | **Full version history** with rollback option in UI                           |
| **Compliance Traceability** | Manual reviewer logging                                       | Logs: `doc_id`, `hash`, `signature_id`, `reviewer_id`, `timestamp`, `score`   |
| **Cost Control**            | Risk of reprocessing, especially with unchanged files         | **Embedding deduplication** and Lambda batching reduce cost                   |
| **Operational Overhead**    | Needs orchestration scripts and embed retry tools             | Fully serverless: Box → EventBridge → Lambda → API Gateway                    |
| **Observability**           | Limited logs; manual debugging                                | Central job DB + optional email/SNS alerts for failures                       |
| **Extensibility**           | Requires manual UI integration for rerun, feedback, standards | Extensible via JSON standards DB + prompt selector module                     |
| **Deployment Options**      | Scripted or manually deployed Flask app + Lambda functions    | **Fully deployable via CDK / Terraform / Serverless Framework**               |

---

### ✅ Summary Recommendations

| Use Case                              | Best Fit Architecture                           |
| ------------------------------------- | ----------------------------------------------- |
| Prototyping or low-volume workflows   | Box + S3 Pattern (V2.5)                         |
| Audit-ready, large-scale ops          | **Managed Pipeline Pattern**                    |
| Frequent doc updates or OCR risk      | Managed Pattern with hash check and retry logic |
| Need UI decoupling and status polling | Managed Pipeline Pattern                        |

