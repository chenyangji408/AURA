## AURA Platform -A Single-Cell Annotation System Based on Large Language Model Debate
[简体中文](README.md) | [English](README-EN.md)

> 📄 **Paper**: AURA: A Multi-LLM Debate Framework for Interpretable Single-Cell Annotation (under review)

---

## 📋 Table of Contents

- Project Introduction

- Core Features

- System Architecture

- Installation and Deployment

- User Guide

- API Configuration & System Settings

- AURA Engine Details

- Frequently Asked Questions (FAQ)

- Contact Information

---

## 🎯 Project Introduction

AURA is an interactive single-cell RNA sequencing  data analysis platform based on R Shiny. It integrates an advanced multi-model debate engine to achieve intelligent and automated cell type annotation.

### Core Highlights

- 🤖 **Multi-Model Debate Engine**: Integrates many Large Language Models to enhance annotation accuracy through a three-round debate mechanism.

- 🎨 **Interactive Visualization**: Requires no coding; all steps can be completed entirely through user interface interactions.

- 📊 **Comprehensive Analysis Workflow**: A one-stop solution encompassing data loading, quality control (QC), dimensionality reduction, clustering, and cell annotation.

- 🗄️ **Multi-Database Integration**: Integrates biological databases including CellMarker, PanglaoDB, gprofiler2, and clusterProfiler.

- 🔧 **Autonomous Candidate Vocabulary**: An LLM integrates five knowledge resources (PanglaoDB, CellMarker, scType, gprofiler2, clusterProfiler) to automatically construct tissue-specific candidate cell types, with customization supported.

- 📈 **Batch Processing**: Supports annotation strategies such as batch mode and cluster-by-cluster mode.

---

## 🚀 Core Features

### 1. Data Processing Module

#### Data Upload

- **Flexible Import Methods**:
  
  - File browser selection (visual operation)
  
  - Manual path input (rapid input)
  
  - Path validation function (ensures directory accuracy)

- **Data Preview**: Real-time display of basic information, including cell count and gene count.

#### Quality Control

- **AI Intelligent Recommendation**: Invokes LLMs to automatically recommend optimal QC parameters.

- **Manual Configuration**: Supports custom thresholds for gene count, UMI count, and mitochondrial proportion.

- **Skip QC**: A fast-track option for pre-filtered data.

- **Visual Feedback**: Real-time display of data distribution before and after filtering.

#### Normalization and Dimensionality Reduction

- **Normalization Processing**: LogNormalize, ScaleData.

- **Highly Variable Gene Identification**: Automated screening of highly variable genes.

- **Dimensionality Reduction Analysis**: PCA, UMAP, t-SNE.

- **Batch Effect Correction**: Employs the Harmony algorithm to eliminate batch effects.

#### Clustering Analysis

- **AI Parameter Recommendation**: Intelligently recommends the optimal resolution and Dims range.

- **Multi-Resolution Exploration**: Supports a resolution range of 0.1 to 2.0.

- **Clustering Tree Visualization**: Utilizes Clustree to display clustering relationships across different resolutions.

- **Result Export**: Supports exporting the post-clustering Seurat object.

### 2. AURA 2.0 Multi-Model Debate Engine

#### Three-Round Debate Mechanism

```
Round 1: Initial Review Debate
├─ Debater A (Spark): Provides preliminary judgment based on marker genes and database evidence.
└─ Debater B (Ernie): Analyzes independently and provides its own judgment.

Round 2: Cross-Examination
├─ Debater B cross-examines Debater A's viewpoints.
└─ Debater A cross-examines Debater B's viewpoints.

Round 3: Referee Adjudication
└─ Referee (DeepSeek): Synthesizes arguments and evidence from both parties to deliver the final adjudication.
```

#### Supported AI Models

The following data is based on a single round of testing:

| **Model Name**                  | **Overall Accuracy** | **Co-expression Ratio** | **Time (minutes)** | **Cost (CNY)** | **Total Tokens** |
| ------------------------------- | -------------------- | ----------------------- | ------------------ | -------------- | ---------------- |
| DeepSeek (deepseek-chat)        | 83.97%               | 11.54%                  | 4.70               | ¥0.10          | 62,347           |
| Spark (4.0Ultra)                | 83.88%               | 2.40%                   | 2.41               | ¥0.67          | 70,384           |
| GLM (glm-4.5-x)                 | 83.88%               | 3.80%                   | 15.82              | ¥0.20          | 88,890           |
| Qwen (qwen-plus)                | 81.62%               | 10.10%                  | 7.79               | ¥0.07          | 84,945           |
| Ernie (ernie-4.5-turbo)         | 81.53%               | 2.40%                   | 3.37               | ¥0.25          | 61,230           |
| Kimi (kimi-k2-turbo-preview)    | 81.53%               | 2.40%                   | 9.34               | ¥0.22          | 63,095           |
| Hunyuan (hunyuan-turbos-latest) | 80.81%               | 2.40%                   | 18.81              | ¥0.12          | 47,933           |
| Minimax (MiniMax-M2-Stable)     | 78.81%               | 2.40%                   | 4.54               | ¥1.77          | 48,540           |
| Doubao (doubao-seed-1.6-flash)  | 35.81%               | 15.35%                  | 3.48               | ¥0.04          | 55,717           |
| Stepfun (step-2-mini)           | 13.26%               | 9.60%                   | 1.86               | ¥1.69          | 73,690           |

> Note: Costs are in CNY; Table 2 of the paper reports them uniformly in USD.

### 3. Database Integration

1. **gprofiler2**
   
   - Function: GO/KEGG/Reactome functional annotation.
   
   - Role: Provides pathway-level functional evidence.

2. **clusterProfiler**
   
   - Function: In-depth KEGG pathway analysis.
   
   - Role: Reveals cellular functional characteristics and metabolic pathways.

3. **PanglaoDB**
   
   - Data Scale: 209 cell types, 8000+ marker genes.
   
   - Role: Provides a broad-spectrum foundation for cell type markers.

4. **CellMarker**
   
   - Data Scale: 113,000+ records, authoritative manual curation.
   
   - Role: Provides the most authoritative cell marker-to-type associations.
   
   - Optimization: Built-in local fallback mechanism to prevent API rate limiting.

5. **scType**
   
   - Features: Tissue-specific markers, including positive and negative markers.
   
   - Role: Facilitates precise annotation for specific tissues.

### 4. Visualization Features

#### Diverse Chart Types

- UMAP-AURA Annotation Plot

- t-SNE-AURA Annotation Plot

- QC Violin Plot

- Sample Distribution Plot

- Feature Gene Expression Plot

- Marker Gene Dot Plot

- Cell Type Violin Plot

- Cell Type Ridge Plot

- Sample Cell Type Stacked Bar Chart

- QC Scatter Plot

#### Interactive Operations

- **One-Click Generation**: Generate corresponding charts with a single button click.

- **Real-Time Preview**: Instantly view visualization results on the right panel.

- **High-Resolution Export**: Supports downloading print-quality images.

### 5. System Management

#### API Management

- **Batch Testing**: One-click functionality to test the connection status of all AI models.

- **Connection Diagnostics**: Real-time display of each model's availability.

#### Dependency Management

- **Automatic Detection**: Intelligently identifies missing R packages.

- **One-Click Installation**: Automatically installs all mandatory dependencies.

- **Re-Verification**: Validate dependency integrity at any time.

---

## 💻 Installation and Deployment

### System Requirements

- **R Version**: ≥ 4.5.1

- **Operating System**: Windows

- **Memory**: Recommended ≥ 8GB

- **Network**: Internet access required to invoke AI model APIs.

### Launching the Application

Click the "Run App" button within RStudio.

### Dependency Package Installation

Please install the required dependencies before accessing the platform, or click 'Install Missing Packages' in System Settings later.

---

## 📖 User Guide

### Interface Structure

The AURA platform consists of the following 7 functional pages:

1. **Data Upload Page** - Data import and basic information overview.

2. **Quality Control Page** - QC parameter configuration and data filtering.

3. **Dimensionality Reduction Page** - PCA, Harmony, UMAP, and t-SNE dimensionality reduction.

4. **Clustering Analysis Page** - Cell clustering and parameter optimization.

5. **Visualization Page** - Generation and display of various charts.

6. **AURA Analysis Page** - AI-driven intelligent cell annotation.

7. **System Settings Page** - API configuration and dependency management.

---

### Complete Operational Workflow

**Note**: Before entering the platform, ensure that the target directory contains a subfolder named `hg19`, which must include the following three files: `barcodes.tsv`, `genes.tsv`, and `matrix.mtx`. Ensure APIs are properly configured.

#### Step 1: Data Upload

1. **Navigate to the Data Upload Page.**

2. **Select Data Import Method**:
   
   - **Method A**: Click the **"Select Data Directory"** button to choose the data folder via the file browser (unavailable if a manual path is already inputted; please clear the manual path field first).
   
   - **Method B**: Manually enter the data directory path.
     
     - After entering the path, click the **"Verify Manual Path"** button.

3. **Click the "Load Data" button** to import the dataset into the platform.

4. **Review basic data information on the right panel**:
   
   - Cell count
   
   - Gene count
   
   - Sample information

*If data needs to be reloaded, please click the Reset Data button.*

---

#### Step 2: Quality Control (QC)

1. **Navigate to the Quality Control Page** (via the left-hand menu).

2. **Configure QC Parameters**:
   
   **Method A: AI Intelligent Recommendation**
   
   - Click the **"Get QC Recommendation"** button.
   
   - The system will invoke an LLM to analyze data characteristics and auto-fill the recommended parameters.
   
   **Method B: Manual Input**
- Directly input parameters based on domain experience:
  
  - Minimum Gene Count
  
  - Maximum Gene Count
  
  - Minimum UMI Count 
  
  - Maximum UMI Count 
  
  - Maximum Mitochondrial Proportion 
  
  **Method C: Skip QC**

- If the data has already been pre-processed, click the **"Skip QC"** button.
3. **Apply QC Filtering**:
   
   - Click the **"Apply Filter"** button.
   
   - The right panel will display the post-QC data distribution plots.

---

#### Step 3: Dimensionality Reduction

1. **Navigate to the Dimensionality Reduction Page.**

2. **Data Preprocessing** (click the following buttons sequentially):
   
   - **"Run Data Normalization"** - Executes LogNormalize on the expression matrix.
   
   - **"Find Variable Features"** - Identifies highly variable genes.
   
   - **"Scale Data"** - Executes ScaleData normalization.

3. **Adjust Principal Components**:
   
   - Specify the number of PCA principal components in the input box.

4. **Execute Dimensionality Reduction**:
   
   - Click **"Run PCA"** - Executes Principal Component Analysis.
   
   - Click **"Run Harmony Batch Correction"** - Eliminates batch effects.

5. **Review Results**:
   
   - The right panel will display PCA and Harmony visualization plots.

---

#### Step 4: Clustering Analysis

1. **Navigate to the Clustering Analysis Page.**

2. **Configure Clustering Parameters** (Two Methods):
   
   **Method A: AI Intelligent Recommendation (Recommended)**
   
   - Click the **"Get API Recommendation"** button.
   
   - The system will invoke an LLM to analyze data characteristics and auto-fill recommended parameters (Resolution, Dims range).
   
   **Method B: Manual Adjustment**
- Manually configure the input boxes:
  
  - Resolution
  
  - Dims Range
3. **Execute Clustering**:
   
   - Click the **"Run Clustering Analysis"** button.

4. **Generate Visualization Charts** (Optional, click as needed):
   
   - **"Plot Elbow Graph"** - Review the optimal number of principal components.
   
   - **"Run UMAP and t-SNE"** - Generate UMAP and t-SNE dimensionality reduction plots.
   
   - All charts will display in real-time on the right panel.

5. **Export Clustering Results**:
   
   - Click the **"Export Clustering Results"** button.
   
   - Download the clustered Seurat object or metadata.

---

#### Step 5: AURA Intelligent Annotation

**Operational Steps**:

1. **Navigate to the AURA Analysis Page.**

2. **Input Configurations**:
   
   **A. Select AI Models**(It is recommended to select DeepSeek Fast (deepseek-chat) as the Judge model, and Spark (4.0Ultra) and Ernie (ernie-4.5-turbo) as the Debater models.)
   
   - **Referee Model**: Select a model to serve as the final adjudicator.
   
   - **Debater A**: Select the primary debater model.
   
   - **Debater B**: Select the secondary debater model.
   
   **B. Select Tissue Type Template**
- The candidate vocabulary is automatically constructed by an LLM integrating five knowledge resources; it can be adjusted as follows:

- **Custom Template**:
  
  - Click **"Edit"** to manually modify cell types and marker genes.
  
  - Alternatively, click **"Upload CSV"** to import a candidate cell type file.

- Click **"Save as Default"** to set the current candidate vocabulary as the default configuration.

- Click **"Download"** to save the candidate vocabulary locally.
3. **Initiate AURA Analysis**:
   
   - Click the **"Start AURA Analysis"** button.
   
   - The system will automatically execute the three-round debate workflow:
     
     - **Round 1**: Debater A and Debater B analyze independently to provide preliminary judgments.
     
     - **Round 2**: Both parties cross-examine each other's viewpoints.
     
     - **Round 3**: The referee synthesizes opinions and issues the final adjudication.

4. **Review Analysis Results**:
   
   **A. Three-Round Analysis Process** (Displayed at the bottom of the page)
   
   - Round 1: Preliminary judgments from Debater A and B.
   
   - Round 2: Cross-examination discourse.
   
   - Round 3: The referee's final adjudication and rationale.
   
   **B. Analysis Results**
- Cell type for each cluster.

- Average confidence level.
  
  **C. Downstream Analysis Recommendations**

- The system provides subsequent analysis suggestions based on the annotation results.
5. **Export Annotation Results** (Bottom of the page):
   
   - **Export as CSV**: Cell type annotation table.
   
   - **Export as RDS**: Complete Seurat object (including annotation metadata).

---

#### Step 6: Visualization

1. **Navigate to the Visualization Page.**

2. **Select Chart Type**:
   
   - UMAP Plot (Colored by cell type)
   
   - t-SNE Plot (Colored by cell type)
   
   - Violin Plot
   
   - Feature Plot
   
   - Dot Plot
   
   - Heatmap
   
   - Clustree

3. **Generate Chart**:
   
   - Select the desired chart type.
   
   - Click the **"Generate Chart"** button.
   
   - The right panel will update in real-time with the corresponding visualization.

4. **Download Chart**:
   
   - Right-click the chart to save as an image.
   
   - Alternatively, use the export function to save a high-resolution image.

---

## 🔑 API Configuration & System Settings

### Obtaining API Keys

| **Model** | **Official Website**                                                          |
| --------- | ----------------------------------------------------------------------------- |
| DeepSeek  | [https://platform.deepseek.com](https://platform.deepseek.com/)               |
| Kimi      | [https://platform.moonshot.cn](https://platform.moonshot.cn/)                 |
| GLM       | [https://open.bigmodel.cn](https://open.bigmodel.cn/)                         |
| Doubao    | [https://console.volcengine.com](https://console.volcengine.com/)             |
| Qwen      | [https://dashscope.console.aliyun.com](https://dashscope.console.aliyun.com/) |
| Hunyuan   | https://cloud.tencent.com/product/hunyuan                                     |
| Ernie     | [https://developer.baidu.com/](https://developer.baidu.com/)                  |
| Stepfun   | [https://platform.stepfun.com/](https://platform.stepfun.com/)                |
| Minimax   | https://www.minimaxi.com/platform_overview                                    |
| Spark     | [https://www.xfyun.cn/](https://www.xfyun.cn/)                                |

### Configuration Method

#### Method 1: Modify Source Code

Locate the following code block in the `AURA.R` file and modify it directly:

R

```
# Set API key environment variables (if not set)
if (Sys.getenv("DEEPSEEK_API_KEY") == "") {
  Sys.setenv(DEEPSEEK_API_KEY = "Your_API_Key")
}
if (Sys.getenv("KIMI_API_KEY") == "") {
  Sys.setenv(KIMI_API_KEY = "Your_API_Key")
}
if (Sys.getenv("GLM_API_KEY") == "") {
  Sys.setenv(GLM_API_KEY = "Your_API_Key")
}
if (Sys.getenv("DOUBAO_API_KEY") == "") {
  Sys.setenv(DOUBAO_API_KEY = "Your_API_Key")
}
if (Sys.getenv("QWEN_API_KEY") == "") {
  Sys.setenv(QWEN_API_KEY = "Your_API_Key")
}
if (Sys.getenv("HUNYUAN_API_KEY") == "") {
  Sys.setenv(HUNYUAN_API_KEY = "Your_API_Key")
}
if (Sys.getenv("ERNIE_API_KEY") == "") {
  Sys.setenv(ERNIE_API_KEY = "Your_API_Key")
}
if (Sys.getenv("STEPFUN_API_KEY") == "") {
  Sys.setenv(STEPFUN_API_KEY = "Your_API_Key")
}
if (Sys.getenv("SPARK_API_KEY") == "") {
  Sys.setenv(SPARK_API_KEY = "Your_API_Key")
}
if (Sys.getenv("MINIMAX_API_KEY") == "") {
  Sys.setenv(MINIMAX_API_KEY = "Your_API_Key")
}
```

### System Settings

1. **Navigate to the System Settings Page.**

2. **API Configuration**:
   
   - Input the API keys for the respective AI models.
   
   - Click the **"Test All APIs"** button.
   
   - Detect unreachable models.
   
   - Review test results and connection statuses.

3. **Dependency Package Management**:
   
   - Click the **"Install Missing Packages"** button.
   
   - The system will automatically detect and install operational dependencies.
   
   - Click the **"Re-check"** button to re-verify dependency completeness.

4. **Other Settings**:
   
   - Adjust the number of CPU cores utilized during runtime.
   
   - Clear cache.

---

## 🤖 AURA Engine Details

### Mechanism of Action

#### 1. Knowledge Base Construction

The core objective of the knowledge base constructor is to transform single-cell data into structured biological evidence, establishing a reliable inferential foundation for Large Language Models (LLMs). The construction pipeline comprises the following six steps:

- **Step 1: Marker Gene Extraction.** Dynamically invokes Seurat's `FindAllMarkers` function to accurately identify differentially expressed genes across cell clusters using specific thresholds (positive markers only, min.pct=0.25, logfc.threshold=0.25).

- **Step 2: PanglaoDB Matching.** Aligns marker genes with PanglaoDB, computing match scores to output the most analogous cell type (e.g., highly matched CD8+ T cells).

- **Step 3: CellMarker Retrieval.** Queries CellMarker to extract associated cell types and tissue origins, incorporating a local fallback mechanism to bypass API rate limits.

- **Step 4: scType tissue-specific matching.** Uses scType tissue-specific marker rules to verify candidate cell types against the tissue context.

- **Step 5: Pathway Enrichment Analysis.** Utilizes clusterProfiler to execute GO and KEGG analyses, illuminating the specific biological functional characteristics of cell clusters.

- **Step 6: SuperPrompt Integration.** Structures the aforementioned multi-dimensional evidence (marker genes, database matching, literature support, and pathway analysis) into a SuperPrompt. This serves as the direct input for the subsequent LLM debate engine, ensuring comprehensive and accurate reasoning.

#### 2. Three-Round Debate Workflow

**Round 1: Initial Review Debate**

- Debater A and Debater B simultaneously receive identical evidence.

- Both independently analyze and output cell type judgments.

- Output Format: JSON (includes cell type, rationale, and key genes).

**Round 2: Cross-Examination**

- Debater B reviews Debater A's judgment and raises queries/objections.

- Debater A reviews Debater B's judgment and raises queries/objections.

- Primary Focus: Completeness of the evidence chain, alternative interpretations, and logical consistency.

**Round 3: Referee Adjudication**

- The Referee synthesizes the viewpoints and cross-examinations of both parties.

- Evaluates evidence weighting and inferential logic.

- Delivers the final judgment and corresponding confidence score.

#### 3. Quality Assessment

Traditional single-cell annotation evaluation typically relies on simple accuracy as the primary metric. However, this approach exhibits notable limitations:

1. **Granularity Mismatch**: The Gold Standard label (e.g., "Memory CD4 T") and the predicted label (e.g., "T cell") may exist at different biological hierarchical levels. Simple string matching penalizes hierarchical variance as errors.

2. **Assessment Inequity**: Different methodologies may output results of varying granularities; coarse-grained methods inherently score higher "accuracy."

3. **Inability to Differentiate Error Severity**: Misclassifying a "CD4 T" as a "CD8 T" (same T cell lineage) is biologically vastly different from misclassifying it as a "B cell" (entirely different lineage).

Drawing upon assessment methodologies from top-tier publications such as GPTCelltype (Hou et al., 2024, Nature Methods), AURA implements a dual-granularity assessment system, reporting both coarse-grained accuracy and fine-grained hierarchical matching results simultaneously.

**Core Concept**: Construct a Cell Type Ontology Tree to execute matching assessments based on hierarchical relationships.

---

## ❓ Frequently Asked Questions (FAQ)

### Q1: What should I do if an API call fails?

**A:** Verify the following parameters:

1. Is the API key correct?

2. Is the network connection stable?

3. Has the API usage quota been depleted?

4. Attempt switching to an alternative model.

### Q2: How can I resolve inaccurate annotation results?

**A:**

1. Assess the quality of the selected marker genes.

2. Adjust the clustering resolution.

3. Review and adjust the candidate cell types.

4. Conduct a manual review and correct as necessary.

### Q3: How do I adjust candidate cell types?

**A:** Navigate to the **AURA Analysis** page:

1. Review the candidate cell types generated by the LLM from the knowledge resources.

2. Click "Edit" to adjust candidate types and marker genes.

4. Save and apply the configuration.

### Q4: How do I export the results?

**A:** After executing the AURA analysis, you can export the annotation results in CSV or RDS formats at the bottom of the AURA Analysis page.

### Q5: Why am I unable to click the "Select Data Directory" button?

**A:** Please ensure that a manual directory path has not been entered. If a manual path is present in the input box, please clear it first.

---

## 📧 Contact Information

- **Author**: chen yangji

- **GitHub**: [chenyangji408](https://github.com/chenyangji408)

---

## 🙏 Acknowledgements

We extend our gratitude to the following open-source projects and databases:

- [Seurat](https://satijalab.org/seurat/) - Single-cell analysis framework

- [Shiny](https://shiny.rstudio.com/) - Interactive Web application framework

- [CellMarker](http://117.50.127.228/CellMarker/index.html) - Cell marker gene database

- [PanglaoDB](https://panglaodb.se/) - Single-cell database

- [gprofiler2](https://biit.cs.ut.ee/gprofiler/) - Functional enrichment analysis

- [clusterProfiler](https://yulab-smu.top/biomedical-knowledge-mining-book/) - Pathway enrichment analysis
