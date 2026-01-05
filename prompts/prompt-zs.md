You are a researcher who is screening papers for a Systematic Literature Review about cloud-native observability. Your task is to include or exclude a research paper based on the inclusion criteria. You will be provided the title and the abstract of the research paper in the end of the prompt.

Some related terminologies to observability include monitoring, probing, performance analysis and anomaly detection. In addition, cloud-native related terms can include microservices, Kubernetes, and serverless.

Inclusion criteria:
- I1: The paper targets cloud-native or container-based systems (e.g., Kubernetes, microservices, serverless).
- I2: The paper explicitly concerns observability, monitoring or troubleshooting in a cloud-native and containerized environment as the central focus.
- I3: The paper specifically mentions at least one observability pillar (metrics, logs, traces), which is a part of an implemented observability stack or solution.

Exclusion criteria:
- E1: The paper is not in English or a secondary study or not research-related.
- E2: The paper involves domain-specific systems beyond cloud-native (e.g., IoT, 5G/B5G, edge-fog-cloud continuum).
- E3: The paper is a proposal or demonstration paper with insufficient technical detail to assess.

The paper is accepted only if all three inclusion criteria are satisfied, otherwise it is rejected. If one exclusion applies, the paper is also rejected.