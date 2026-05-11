AWS ML + AI Application Delivery Roadmap
A practical curriculum for moving from algorithms to production endpoints
Scope: classical ML, MLOps, GenAI applications, and API exposure for downstream integration
Team size	2 people
Recommended duration	14 weeks
Delivery approach	One end-to-end project at a time, with reusable platform components
End state	A portfolio of deployable ML and GenAI services with documented endpoints

Prepared for peer sharing and team execution planning
 
1. Executive summary
This roadmap is designed for a two-person team that wants to learn and deliver real-world machine learning and AI solutions on AWS, starting from algorithm selection and ending with production-ready endpoints that other applications can call.
The curriculum is split into two tracks that share common engineering standards: a classical ML and MLOps track built primarily on Amazon SageMaker, and a GenAI application track built primarily on Amazon Bedrock.
The sequence is intentional. Early projects focus on classification and forecasting because they teach the core delivery mechanics: data preparation, training, evaluation, registration, deployment, monitoring, and API exposure. Later projects introduce unsupervised learning, anomaly detection, retrieval-augmented generation, and AI agents with business actions.
By the end of the roadmap, the team should be able to:
- Choose an appropriate algorithm family for a business problem.
- Build reproducible training and evaluation workflows.
- Register, approve, deploy, and monitor models on SageMaker.
- Expose prediction and chat endpoints for integration with other applications.
- Build GenAI applications that use knowledge retrieval, actions, and safety controls.
Guiding principles
- Build one complete solution at a time instead of studying algorithms in isolation.
- Use the same platform pattern repeatedly so the team develops production reflexes.
- Stop each project at a stable service boundary: a documented endpoint, monitoring, and a handover note.
- Keep the solution cloud-native where AWS adds leverage, but write model code and application code in a portable way.
2. Two-person operating model
A two-person team can deliver this roadmap successfully if responsibilities are clear, interfaces are shared, and both members cross-train enough to cover each other.
Role	Primary responsibility	Secondary responsibility
Engineer A - ML / MLOps lead	Data preparation, feature engineering, model training, evaluation, SageMaker pipelines, model packaging, monitoring setup	Support application integration, API contract review, documentation of model behavior
Engineer B - AI app / integration lead	API design, lightweight application layer, Lambda functions, Bedrock orchestration, endpoint consumers, demo UI and Postman collection	Support experiments, evaluation reports, deployment automation, and runbook authoring
Shared responsibilities	Architecture decisions, backlog prioritization, cost review, security basics, IAM review, demo preparation, retrospectives	Cross-training, peer review, defect triage, release readiness, stakeholder communication
Weekly cadence
- Monday: planning and technical design for the week.
- Mid-week: joint review of experiments, pipeline status, and integration progress.
- Friday: demo, endpoint validation, defect log update, and documentation closure.
3. Reference architecture patterns
Pattern A: Classical ML + MLOps on SageMaker
Layer	Recommended AWS services	Purpose in this roadmap
Storage and source data	Amazon S3; optional AWS Glue or Athena	Store curated datasets, labels, baseline outputs, evaluation reports, and monitoring artifacts
Feature layer	Amazon SageMaker Feature Store	Create reusable features for training and online inference consistency
Training and orchestration	Amazon SageMaker training jobs; SageMaker Pipelines	Run preprocessing, training, evaluation, conditional approval, and deployment steps
Governance	SageMaker Model Registry; optional Model Cards	Track model versions, metrics, lineage, and promotion status
Serving	SageMaker real-time endpoint; inference pipeline where needed	Expose low-latency prediction services with optional preprocessing or postprocessing
Operations	SageMaker Model Monitor; SageMaker Clarify; Amazon CloudWatch	Track drift, model quality, feature attribution change, and operational health
Consumer interface	Amazon API Gateway + AWS Lambda or direct application calls	Expose a stable API contract for other applications to integrate with
Pattern B: GenAI application on Bedrock
Layer	Recommended AWS services	Purpose in this roadmap
Knowledge source	Amazon S3 and curated documents	Provide internal data for retrieval-augmented generation use cases
Retrieval	Amazon Bedrock Knowledge Bases	Connect private data to GenAI responses without building the entire retrieval stack manually
Generation	Amazon Bedrock model inference	Run text generation, summarization, classification, and embedding-backed responses
Tool use and actions	Amazon Bedrock Agents + AWS Lambda	Allow the application to call business functions such as ticket creation, lookup, or task execution
Safety and governance	Amazon Bedrock Guardrails	Filter harmful content and help protect sensitive information in prompts and responses
Consumer interface	Amazon API Gateway + Lambda or lightweight web application	Expose chat or task endpoints for downstream channels or applications
Operations	CloudWatch logs and traces plus application metrics	Observe latency, errors, prompt behavior, and action success rates
Note: API Gateway and Lambda are included as the most common edge pattern for stable external integration; direct internal application calls to SageMaker or Bedrock are also possible where architecture policy allows.
4. Project portfolio and learning sequence
The portfolio below is ordered to build practical competence progressively. Each project ends with a tested endpoint, an evaluation note, a deployment artifact, and an operational handover page.
Project	Problem type	Algorithms or method	AWS delivery focus	Target endpoint(s)
1. Customer churn prediction	Binary classification	Logistic Regression, Random Forest, XGBoost	SageMaker pipeline, Feature Store, Model Registry, real-time endpoint, Model Monitor	POST /predict, GET /health, GET /model-info
2. Loan default / credit risk scoring	Binary classification with governance emphasis	Logistic Regression, XGBoost, CatBoost	Clarify, model approval workflow, threshold tuning, endpoint contract	POST /score, GET /health
3. Demand forecasting	Time-series / supervised forecasting	Feature-engineered XGBoost baseline; optional DeepAR follow-up	Scheduled retraining, forecast endpoint, drift checks	POST /forecast, GET /health
4. Fraud or anomaly detection	Rare event / anomaly detection	Isolation Forest, Autoencoder, XGBoost	Real-time scoring, alert thresholds, post-processing rules	POST /detect, GET /health
5. Segmentation or recommendation	Unsupervised clustering or ranking	K-Means + PCA or recommendation model	Batch pipeline plus serving path for assignment or recommendation	POST /segment or POST /recommend
6. Internal knowledge assistant	RAG application	Bedrock Knowledge Bases plus FM inference	Document ingestion, retrieval, response endpoint, guardrails	POST /ask, GET /health
7. Customer service agent with actions	Agentic AI application	Bedrock Agents with Lambda action group	Action orchestration, session handling, guardrails, app integration	POST /chat, POST /action, GET /health
5. Fourteen-week execution plan
The schedule below assumes the team is learning while delivering. If the team already has strong AWS experience, this can be compressed; if the team is balancing client work, it can be expanded to 16 to 18 weeks.
Week	Focus	Main activities	Deliverables
Week 1	Foundation and environment setup	Define repo structure, IAM roles, S3 layout, coding standards, experiment template, endpoint contract template, cost guardrails	Working repository, deployment checklist, architecture baseline, shared naming convention
Week 2	Project 1 - churn data and baseline	Prepare data, build baseline Logistic Regression and Random Forest, define features, agree success metrics	Exploration notebook, baseline metrics, feature list, initial API schema
Week 3	Project 1 - productionization	Train XGBoost candidate, create SageMaker Pipeline, register model, deploy real-time endpoint, add monitoring	Churn endpoint, pipeline definition, model card summary, test evidence
Week 4	Project 2 - credit risk framing	Design risk use case, calibration approach, fairness checkpoints, threshold rules, create evaluation plan	Risk scoring design note, Clarify checklist, endpoint contract
Week 5	Project 2 - build and deploy	Train models, compare metrics, add explainability, register best model, expose scoring endpoint	Credit risk service, explanation report, release note
Week 6	Project 3 - forecasting baseline	Engineer time features, create time-aware split, train baseline, define forecast horizon and response schema	Forecast baseline report, pipeline draft, response payload spec
Week 7	Project 3 - productionization	Automate retraining flow, expose forecast endpoint, add quality checks and operational logging	Forecast service, scheduled runbook, monitoring dashboard notes
Week 8	Project 4 - fraud / anomaly detection	Prepare imbalanced data strategy, compare anomaly and supervised approaches, define alert thresholds	Fraud scoring comparison note, threshold matrix
Week 9	Project 4 - deploy and harden	Deploy best candidate, integrate post-processing rules, add monitoring and rollback plan	Fraud endpoint, rollback note, ops checklist
Week 10	Project 5 - segmentation or recommendation	Choose track based on business relevance, build batch pipeline, define serving pattern	Segmentation or recommendation artifact, endpoint or batch contract
Week 11	Project 6 - knowledge assistant	Prepare documents, configure Bedrock Knowledge Base, test retrieval quality, add guardrails	Ask endpoint, prompt templates, retrieval validation notes
Week 12	Project 6 - app integration	Wrap knowledge service behind API Gateway or application layer, add response shaping and error handling	Integrated knowledge assistant service, API tests
Week 13	Project 7 - agent with actions	Create Bedrock Agent, build Lambda action group, test session handling and function calls	Chat endpoint, action contract, action logging pattern
Week 14	Portfolio hardening and showcase	Consolidate documentation, standardize deployment scripts, demo end-to-end flows, create final runbooks and backlog for next phase	Shareable portfolio package, support runbooks, demo deck inputs
6. Definition of done for each project
Category	Minimum completion criterion
Business framing	Clear objective, target user, decision owner, success metric, and latency expectation.
Data package	Versioned dataset or retrieval source list, data dictionary, split strategy, and leakage checks.
Experiment package	Baseline model, candidate model comparison, evaluation summary, and reproducible code.
Deployment package	Training pipeline or application deployment script, environment variables, IAM assumptions, and release notes.
Service contract	Endpoint path, sample request and response, expected error cases, and health check.
Operations package	Monitoring setup, alert thresholds, rollback plan, and lightweight runbook.
Knowledge transfer	Short demo, architecture sketch, known limitations, and backlog for next iteration.
7. Recommended repository and delivery structure
Use one mono-repo or a tightly coordinated project workspace so shared standards remain visible. A simple structure is below.
root/
  docs/
    architecture/
    runbooks/
    api-contracts/
  datasets/
    raw/
    curated/
  projects/
    churn/
    credit-risk/
    forecasting/
    fraud/
    segmentation-or-reco/
    knowledge-assistant/
    service-agent/
  infra/
    sagemaker/
    bedrock/
    api-gateway-lambda/
  tests/
  postman/
8. Standard endpoint contracts
Keep endpoint design consistent across projects so downstream integration becomes easy. Use JSON payloads, a health endpoint, explicit error messages, and versioned paths where practical.
Service type	Example route	Usage
Prediction service	POST /v1/predict	Accepts business features and returns class, score, and optional explanation fields
Scoring service	POST /v1/score	Accepts customer or transaction features and returns risk or fraud score
Forecast service	POST /v1/forecast	Accepts entity and horizon details and returns projected values for the requested period
Knowledge service	POST /v1/ask	Accepts question and context metadata and returns grounded answer plus source references if exposed
Agent service	POST /v1/chat	Accepts user utterance and session ID and returns response plus any action outcome metadata
Health check	GET /health	Returns service status, version, and optionally model or agent identifier
Model metadata	GET /model-info	Returns active model version, training date, and supported fields where appropriate
9. Metrics to track throughout the roadmap
Model metrics
- Classification: ROC-AUC, PR-AUC, precision, recall, F1, calibration, and threshold-based business impact.
- Forecasting: MAE, RMSE, MAPE where appropriate, plus error by segment and forecast horizon.
- Segmentation: silhouette score or qualitative segment usefulness, plus business interpretability.
- Recommendation: ranking metrics such as precision at K or recall at K, where dataset design allows.
Operational metrics
- Latency, error rate, and endpoint availability.
- Data drift, model quality drift, and feature attribution drift where relevant.
- Prompt failure rate, retrieval quality observations, and action success rate for GenAI applications.
- Change failure rate and mean time to recovery during releases.
10. Common risks for a two-person team and mitigations
Risk	Mitigation
Trying to learn too many services at once	Keep the AWS surface area narrow in the first half: S3, SageMaker, CloudWatch, API Gateway, Lambda, and Bedrock.
Weak documentation discipline	Treat the runbook and endpoint contract as part of the deliverable, not an afterthought.
No rollback or monitoring	Add health checks, logs, and rollback notes before calling a project complete.
Dataset quality issues	Start with known public or cleaned internal datasets and make data validation part of week-level tasks.
Overbuilding the UI	Use Postman, a small demo client, or a very light web front end. The focus is the service boundary.
Single point of failure in the team	Rotate demo ownership and review each other's code and deployment notes every week.
