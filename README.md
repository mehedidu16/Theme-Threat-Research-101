# Event-Themed Threats Research: Case Study on Russia-Ukraine War Themed Website Campaigns
The original code and data are given inside the directories with the same name within the project directory of **Russia-Ukraine-War-Theme**. This document provides an overview of the methodology and results for clustering analysis performed on a dataset of websites. The analysis includes the selection of the optimal number of clusters, feature reduction, and local explanations for cluster assignments. Below is a summary of the key sections and findings.

# A. Details on Selecting Number of Clusters (k)
To determine the optimal number of clusters (k), first, we utilized our baseline evaluation method from **Silhouette Score**, and then for further justification for K-Means, K-Medoids, and Gaussian Mixture Model (GMM) clustering, we employed several evaluation techniques:

**Calinski-Harabasz Score**

Used for K-Means and K-Medoids clustering.

The elbow graph ([A.1](#calinski-harabasz-elbow-graph)) suggests that k=3 is optimal, as the score decreases significantly beyond this point.

![A.1](https://github.com/MarazMia/Theme-Threat-Research-101/blob/main/Russia-Ukraine-War-Theme/Diagrams/caliski_elbow.png)

**Hierarchical Clustering (Dendrogram)**

The dendrogram ([A.2](#dendrogram-graph)) indicates that a Ward linkage distance of 47.5 splits the data into three clusters (k=3).
![A.2](https://github.com/MarazMia/Theme-Threat-Research-101/blob/main/Russia-Ukraine-War-Theme/Diagrams/Dendrogram.png)

**AIC and BIC Scores for GMM**

The elbow graph ([A.3](#aic-bic-graph)) suggests two possible candidates for k: 3 and 5.
![A.3](https://github.com/MarazMia/Theme-Threat-Research-101/blob/main/Russia-Ukraine-War-Theme/Diagrams/AIC_BIC.png)

# B. Feature Reduction Based on Pair-Wise Pearson Correlation Coefficient
A feature correlation heatmap ([B.1](#pearson-corr-heatmap)) was used to identify highly correlated features.
Features with a Pearson correlation coefficient greater than 0.6 were discarded to reduce redundancy and improve model performance.
![B.1](https://github.com/MarazMia/Theme-Threat-Research-101/blob/main/Russia-Ukraine-War-Theme/Diagrams/feature_correlation.png)

# C. Local SHAP Explanation to Disclose Why Any Individual Website Resides in a Particular Cluster
Local explanations for cluster assignments were generated using SHAP (SHapley Additive exPlanations).
Figure ([Local_Exp](#local-exp)) provides a waterfall plot for a random instance from cluster C_2, showing the contribution of
individual features to the cluster assignment. This visualization helps explain why a specific website was assigned to a particular cluster.

The confusion matrix heatmap plot ([C.1](#confusion-matrix-plot)) below suggests a very accurate supervised model using the XGBoost classifier with three cluster labels as classes, which is used as a mapping model on the clustering result.
![C.1](https://github.com/MarazMia/Theme-Threat-Research-101/blob/main/Russia-Ukraine-War-Theme/Diagrams/supervised_model_cm.png)

The global bar plot ([C.2](#global-mean-plot)) of the absolute mean SHAP values reveals the overall highly contributed feature. It is evident from the plot that the features landing_page_size, avg_external_link_len, domain_letter_count, same_landing_domain, unique_external_page_link_count, and unique_internal_page_link_count are some of the top contributing features for all cluster labels.
![Global Absolute Mean Bar](https://github.com/MarazMia/Theme-Threat-Research-101/blob/main/Russia-Ukraine-War-Theme/Diagrams/majority_bar.png)

In figure ([C.3](#local-exp)), we observe the local explanation (i.e., explanation for a single instance) for a random sample from cluster C_2, where we can see three waterfall plots because the dimension of the generated SHAP value is (2118, 28, 3) representing the number of instances fed into the SHAP explainer object, feature number, and class number (cluster). This figure shows why (i.e., which features are making an impact) the individual website is residing in cluster C_2 based on the plots.
![Local Exp](https://github.com/MarazMia/Theme-Threat-Research-101/blob/main/Russia-Ukraine-War-Theme/Diagrams/local_shap.png)


# D. Clusters of Domain Names Based on String Match
We also cluster the websites based on the string matching domain name similarity (95% similarity thresholds), which reveals several websites use same domain name while registering the websites which indicates an attempt from one campaign individual/group just tweaking the top-level domain and keeping the same domain name in all the other websites. Figure ([D.1](#domain-name-cluster)) shows some of the same domain names with frequency that were used in different websites. This finding reveals that some triggered words like **help**, **support**, **help**, and **aid** were frequently used.
![D.1](https://github.com/MarazMia/Theme-Threat-Research-101/blob/main/Russia-Ukraine-War-Theme/Diagrams/domain_string_cluster.png)

# E. Analysis of Top Level Domain(TLD)
Here, we also provide the TLD level analysis, which discloses some patterns. The below image ([E.1](#E.1)) displays overall top 10 TLD usage in the entire dataset. The most frequent ones are .com, .org, .de .ch, and .net. Here, we observe that the majority of the TLDs are country code TLDs (ccTLD), so we further provide a separate bar plot only for the ccTLDs with the one-year registration cost.
![E.1](https://github.com/MarazMia/Theme-Threat-Research-101/blob/main/Russia-Ukraine-War-Theme/Diagrams/all_TLD.png)

This finding from image ([E.2](#E.2))suggests that, as the event mainly happened in the European regions, a significant portion of the websites are also registered from this and the surrounding regions as TLDs like .eu (European Union), .ch (Switzerland), .nl
(Netherlands), .uk (United Kingdom), .at (Austria), .dk (Denmark), and .fr(France) are from the European side.
![E.2](https://github.com/MarazMia/Theme-Threat-Research-101/blob/main/Russia-Ukraine-War-Theme/Diagrams/cc_TLD.png)

