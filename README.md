# For KDD24' Anonymous Rebuttal (Submission ID: 1763)

This is a temporary page to present additional experiment results and analysis for anonymous rebuttal.

Currently this page contains extra rebuttal contents of <b>submission 1763 *Team up GBDTs and DNNs: Advancing Efficient and Effective Tabular Prediction with Tree-hybrid MLPs*</b> in KDD 24'. <b>All used reference No. follow the original ones in the paper</b> if without specification.

**Anchors to detailed response materials**:
- [💬 To R twnd](#twnd)
- [💬 To R pAZD](#pAZD)
- [💬 To R F2J2](#F2J2)
- [💬 To R jHCg](#jHCg)
- [💬 To R LYyH](#LYyH)
- [💬 To R hswh](#hswh)

<a id="twnd"></a>

# 💬 To R twnd 

## QA3: The average ranks (standard deviations) on different imbalance-level scenarios
<!-- <p style="text-align: center;"><b></b></p> -->

|                          | XGBoost       | CatBoost  | MLP       | AutoInt   | DCNv2     | TabNet    | SAINT     | FT-T      | T-MLP     | T-MLP(3)      |
| :----------------------- | :------------ | :-------- | :-------- | :-------- | :-------- | :-------- | :-------- | :-------- | :-------- | :------------ |
| $p < 0.33$ (32 datasets)  | 5\.0(3.0)     | 4\.8(3.2) | 6\.5(2.6) | 5\.4(2.5) | 5\.1(2.6) | 7\.7(2.8) | 6\.0(2.1) | 5\.0(2.4) | 5\.5(3.2) | **4\.1(2.5)** |
| $p < 0.3$ (18 datasets)   | 5\.2(3.4)     | 4\.6(3.1) | 6\.7(2.6) | 4\.6(2.4) | 5\.3(2.6) | 7\.5(2.7) | 6\.9(2.2) | 4\.9(2.3) | 5\.3(3.3) | **3\.8(2.2)** |
| $p < 0.125$ (12 datasets) | **4\.3(3.2)** | 4\.8(3.1) | 6\.4(3.1) | 4\.6(2.6) | 5\.5(2.7) | 7\.3(2.6) | 7\.3(1.5) | 4\.6(2.1) | 5\.8(3.4) | **4\.3(2.1)** |
| $p < 0.05$ (4 datasets)   | **2\.5(1.0)** | 5\.8(3.3) | 5\.5(3.1) | 3\.5(3.0) | 5\.6(2.2) | 7\.5(3.7) | 7\.6(1.5) | 5\.3(2.5) | 6\.1(2.8) | 4\.8(2.5)     |

**Analysis:** We reuse the recently released work TP-BERTa [2] which was comprehensively evaluated on imbalance-class scenarios with 32 imbalanced binary classification datasets from [OPENTABS Database](https://arxiv.org/pdf/2307.04308.pdf). The $p$ denotes the minor-class proportions, i.e., $p=\frac{\text{min}(P, N)}{D}$ ($P$ is positive sample amount, $N$ is the negative one, and $D$ is the dataset size), indicating the imbalance level of a dataset. It can be clearly seen the ensemble version of T-MLP (T-MLP(3)) still holds its superiority on moderate class-imbalance situations. GBDTs dominates the performance in the extremely imbalanced situations (i.e., $p < 0.05$), but T-MLP(3) still outperforms most DNN baselines. Among DNNs, AutoInt[50] exhibits promising performances in the imbalance-class conditions, which may due to its capability of capturing patterns for minority class by manually combining original features to generate new features.

<a id="pAZD"></a>

# 💬 To R pAZD

<b>Q1: Constrained novelty since integration techniques from other fields (i.e., GBDT, vision MLPs, langue model pruning)?</b>

A1: Many successful interdisciplinary works stand on the shoulders of existing techniques from other fields

- Vision Transformer (ViT) incorporated the Transformer architecture to address long-distance pixel interaction in vision tasks.
- TextCNN is a textbook-level model using stacked CNN to realize distant word dependency for sentence classification.
- For tabular data field:
    1. FT-T [23] adapted Transformer and BERT-like inference to tabular data learning.
    2. Recently, TabDDPM and TabR integrated diffusion models and k-Nearest-Neighbors algorithm respectively to tabular data prediction

We follow the same paper style. Techniques from other fields are shoulders to push the progress of research community and sharp tools to solve practical problems.

**Reference**
- VIT: An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale, ICLR, 2021.
- TextCNN: Convolutional Neural Networks for Sentence Classification, EMNLP, 2014.
- TabDDPM: TabDDPM: Modelling Tabular Data with Diffusion Models, ICML, 2023.
- TabR: TabR: Tabular Deep Learning Meets Nearest Neighbors, ICLR, 2024.

## QA2: Efficiency on inference time

<p style="text-align: center;"><b>Inference time overhead against T-MLP on T2G benchmakr</b></p>

| Dataset | GE       | CH      | EY       | CA       | HO       | AD       | OT       | HE        | JA      | HI       | FB       | YE       | avg      | rank      |
| :---------- | :------- | :------ | :------- | :------- | :------- | :------- | :------- | :-------- | :------ | :------- | :------- | :------- | :------- | :-------- |
| MLP         | x 3\.76  | x 1\.07 | x 0\.61  | x 1\.93  | x 1\.55  | x 3\.61  | x 0\.57  | x 0\.75   | x 0\.35 | x 1\.68  | x 1\.09  | x 1\.20  | x 1\.51  | 8\.3(1.9) |
| SNN         | x 4\.90  | x 0\.91 | x 0\.93  | x 2\.64  | x 1\.13  | x 1\.83  | x 3\.10  | x 0\.30   | x 0\.43 | x 3\.35  | x 2\.95  | x 2\.75  | x 2\.10  | 8\.3(1.5) |
| NODE        | x 49\.49 | x 6\.26 | x 27\.61 | x 88\.72 | x 40\.13 | x 12\.44 | x 24\.17 | x 111\.99 | x 6\.97 | x 54\.30 | x 7\.03  | x 13\.21 | x 36\.86 | 7\.0(3.0) |
| AutoInt     | x 22\.12 | x 2\.44 | x 2\.68  | x 23\.09 | x 4\.82  | x 10\.09 | x 5\.62  | x 0\.67   | x 2\.45 | x 23\.91 | x 3\.20  | x 2\.72  | x 8\.65  | 8\.1(2.0) |
| DCNv2       | x 3\.95  | x 7\.87 | x 0\.38  | x 3\.21  | x 2\.43  | x 5\.10  | x 5\.91  | x 0\.85   | x 0\.15 | x 1\.96  | x 1\.56  | x 1\.16  | x 2\.88  | 8\.3(2.2) |
| FT-T        | x 25\.24 | x 4\.02 | x 2\.87  | x 12\.23 | x 9\.51  | x 8\.43  | x 4\.75  | x 2\.17   | x 1\.53 | x 13\.28 | x 6\.36  | x 15\.25 | x 8\.80  | 4\.7(2.6) |
| T2G         | x 38\.98 | x 5\.34 | x 3\.96  | x 33\.54 | x 10\.33 | x 17\.50 | x 13\.67 | x 3\.71   | x 2\.59 | x 52\.67 | x 12\.32 | x 6\.16  | x 16\.73 | 3\.1(1.7) |
| T-MLP       | x 1\.00  | x 1\.00 | x 1\.00  | x 1\.00  | x 1\.00  | x 1\.00  | x 1\.00  | x 1\.00   | x 1\.00 | x 1\.00  | x 1\.00  | x 1\.00  | x 1\.00  | 3\.3(0.8) |
| T-MLP(3)    | x 1\.18  | x 1\.14 | x 1\.16  | x 1\.15  | x 1\.10  | x 1\.13  | x 1\.19  | x 1\.15   | x 1\.08 | x 1\.20  | x 1\.16  | x 1\.10  | x 1\.15  | 2\.0(1.1) |

**Overall Trend:** T-MLP can achieve SOTA competitive results as T2G-Former on its benchmark with an MLP-level (the first row) inference speed, and its ensemble version with 3 MLPs only takes around 15% more time in average, evidently faster than popular Transformer- or attention-based models (e.g., AutoInt, FT-Transformer, T2G-Former). Moreover, benefited from no hyperparameter tuning, T-MLP holds very controllable and stable inference time (all configs are static), while the searched best model configs of other existing tabular DNNs vary drastically as the random seed changes, especially with the large hyperparameter search space, that is why we repeat 15 random seeds and use the average results.

**In-depth Analysis:** Essentially, for DNN part of T-MLP, the single-block MLP process only contains 4 matrix operations (3 matrix multiplications and 1 Hadamard product), here we omit non-parametric activation functions and normalization for clear analysis.
- **operation 1 & 2:** $H = W_fXW_{h1} + b$, where $X \in \mathbb{R}^{F \times d}$ is the embedded input features of a sample, $W_{h1} \in \mathbb{R}^{d \times 2c}$ is transformation on the hidden dimension, $W_f \in \mathbb{R}^{F \times F}$ is transformation on feature dimension in SGU (Eq. 6), $b$ is the bias term combining the ones of $W_f$ and $W_{h1}$;
- **operation 3 & 4:** $\hat{H} = H_{:, :c} \odot H_{:, c:} W_{h2}$, where $\odot$ is Hadamard product and $W_{h2} \in \mathbb{R}^{c \times d}$ is transformation on hidden dimension, $\hat{H}$ is used for final prediction. 
- **For T-MLP ensemble version**, i.e., T-MLP(3), matrix reduction can be simply realized by contacting respective $W_f$, $W_{h1}$, $W_{h2}$ of 3 MLPs into the larger weight matrices once the weights are frozen (during inference), and the same 4 matrix operations can be performed to calculate 3 MLP processes simultaneously.
- Since we uniformly use a sparsity rate of 0.33 (stated in line 1148), i.e., **around 67% values in the MLP weight matrices are zero**, which are sparse and can get inherent further acceleration by CUDA computation optimization.
- For GBDT part, the trained XGBoost is converted into PyTorch tensor computation by [Microsoft Hummingbird compiling tools](https://github.com/microsoft/hummingbird), and this conversion operation has been done during training, in inference it only needs 3-step matrix multiplications with CUDA acceleration to complete the calculation (detailed mechanism illustration in its repo README).

Contrastively, when considering the Transformer architecture that has been widely adopted in many recent SOTA tabular DNNs, each Transformer block (layer) inevitably contains multi-head self-attention (BERT-like) or masked attention (GPT-like) and FFN modules, and the total matrix multiplication time is evidently more than T-MLP. Moreover, the best model config of Transformer-based DNNs often requires several to tens of blocks (layers). 

Consequently, we can observe around 8~16 times inference speedup when using T-MLP. From the perspective of model simplicity and efficiency, using simple XGboost-MLP architecture to reach comparable or competitive results as the heavily tuned SOTA Transformer-based DNNs and GBDTs on their respective dominating benchmark, all achieved with significantly reduced training & inference time, is our primary focus and contribution, which is aimed at strongly practical & industrial applications and green AI.

## QA3: Expanded ablation datasets & analysis

<table style="border-collapse: collapse; border: none; border-spacing: 0px;">
	<caption>
		<b>The detailed ablation on T2G datasets</d>
	</caption>
	<tr>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			T2G Dataset:
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); border-left: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			GE⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			CH⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			EY⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			CA⬇️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			HO⬇️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			AD⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			OT⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			HE⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			JA⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			HI⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			FB⬇️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			YE⬇️
		</td>
	</tr>
	<tr>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			T-MLP
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-left: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.706</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.862</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.717</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.447</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>3.125</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.864</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.814</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.386</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.728</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.729</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>5.667</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>8.768</b>
		</td>
	</tr>
	<tr>
		<td style="border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			w/o sparsity
		</td>
		<td style="border-left: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.681
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.857
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.688
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.450
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			3.136
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.857
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.806
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.377
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.720
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.726
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			5.708
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			8.887
		</td>
	</tr>
	<tr>
		<td style="border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			w/o GBDT FG
		</td>
		<td style="border-left: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.694
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.858
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.692
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.454
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			3.172
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.859
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.809
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.372
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.723
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.728
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			5.736
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			8.799
		</td>
	</tr>
	<tr>
		<td style="border-right: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			w/o both
		</td>
		<td style="border-left: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.676
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.857
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.673
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.460
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			3.169
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.856
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.803
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.373
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.717
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.724
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			5.759
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			8.896
		</td>
	</tr>
	<tr>
		<td style="border-right: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			T-MLP (Neural FG)
		</td>
		<td style="border-left: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.665
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.858
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.699
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.456
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			3.188
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.852
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.809
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.375
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.721
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.718
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			5.861
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			8.925
		</td>
	</tr>
	<tr>
		<td style="border-right: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			w/o sparsity
		</td>
		<td style="border-left: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.647
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.855
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.675
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.456
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			3.205
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.840
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.804
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.372
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.716
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.713
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			5.887
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			8.936
		</td>
	</tr>
</table>


**[Analysis]** There are several overall and subtle observations: 
- Both the sparse MLP structure and the GBDT feature gate are improvement points for T-MLP; 
- MLP sparsity often has a more profound impact than the GBDT feature gate on classification tasks, which may be explained by the underlying consistency between model sparsity and the discrete target nature of classification; 
- The GBDT feature gate plays a more important role in regression since it has the capability of selecting salient features to alleviate the impact of noisy features, which may affect precise regression prediction; 
- Our GBDT feature gate is often a better choice than the previously proposed neural feature gate (Neural FG, proposed for biomedical scenario) [64] on general tabular data prediction.

Similar trend is observed additionally conducted ablations on FT-Transformer (11 datasets) and SAINT (26 datasets) benchmarks, and we will include all detailed ablation results and analysis in the final version, thank you!

## Q5: How are the fixed hyperparameters initially determined? Fig. 2 exhibits different datasets prefer different sparsity level, are the two fine-grained variables, $z_h$ and $z_{in}$ (line 425-426), for sparsity fixed?

A5: (1) Please refer to QA1 of R hswh on how we determine the hyperparameter values, the default ones are listed in the [page bottom](#hswh). (2) We would like to briefly clarity the **fundamental misunderstandings** here. The introduced $z_h$ and $z_{in}$ are learnable binary masks for masking the corresponding values on MLP weight matrices, which sizes are adaptively determined by the sizes of weight matrices. The true & only hyperparameter in sparsification operation is the target sparsity rate, once it is assigned, the method will promise to produce the two variables with the assigned sparsity rate (target ratio of non-zero values) using CoFi pruning [62]. Secondly, as you said (also shown in Fig. 2), datasets vary in appetite of sparsity rates, we provide win statistics of different sparsity rates on T2G benchmark:

<p><b>Win statistics of different T-MLP sparsity rates on 12 T2G datasets</b></p>

| Sparsity rate | 10% | 33% | 50% | 66% | 90% | 100% |
| :------------ | :--: | :--: | :--: | :--: | :--: | :--: |
| Wins          | 0   | 4   | 5   | 2   | 0   | 1    |

Sparsity rate here means how many weights remaining after pruning. The above results show sparsity in T-MLP in often an improvement point, while excessive sparsity can also hurt performance. Therefore, to hold the strength of no hyperparameter tuning and lightweight storage, we keep a fixed sparsity rate of 33% for all datasets (line 449-450) considering both effectiveness and parameter compactness.

<a id="F2J2"></a>

# 💬 To R F2J2

## QA2: Why separate feature selection between training & inference?

<p><b>Comparison with no feature selection separation (*) between training & inference</b></p>

| T2G Dataset:  | GE⬆️   | CH⬆️   | EY⬆️   | CA⬇️   | HO⬇️   | AD⬆️   | OT⬆️   | HE⬆️   | JA⬆️   | HI⬆️   | FB⬇️   | YE⬇️   |
| :------------ | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: |
| T-MLP         | 0\.706 | 0\.862 | 0\.717 | 0\.449 | 3\.125 | 0\.864 | 0\.814 | 0\.386 | 0\.728 | 0\.729 | 5\.667 | 8\.768 |
| T-MLP\*       | 0\.673 | 0\.862 | 0\.708 | 0\.462 | 3\.124 | 0\.864 | 0\.806 | 0\.384 | 0\.726 | 0\.729 | 5\.710 | 8\.792 |
| T-MLP(3)      | 0\.714 | 0\.866 | 0\.747 | 0\.438 | 3\.063 | 0\.867 | 0\.823 | 0\.386 | 0\.732 | 0\.730 | 5\.629 | 8\.732 |
| T-MLP\*(3)    | 0\.684 | 0\.861 | 0\.725 | 0\.446 | 3\.115 | 0\.867 | 0\.819 | 0\.386 | 0\.732 | 0\.729 | 5\.683 | 8\.757 |

**Analysis:** Groups with * are directly trained with GDBT feature frequency as inference (not separating). An overall trend is that on most datasets, separating GBDT feature selection during training and inference often achieves stably better performances. Essentially, this can be explained by an implicit data augmentation mechanism, i.e., **increasing training difficulty by implicitly introducing randomly diverse data facets**. Such mechanism are widely adopted in many classical deep learning techniques, for example, **DropOut technique randomly discards some neuron outputs during training and retains all in inference**, this operation is equivalent to introducing randomness during the training to enrich facets of data hidden states and prevent overfitting; for white noise (Gaussian noise) augmentation, random noise is applied to input tabular data during training and not used in inference. **Similarly, we train GBDT feature selection process by sampling with GBDT feature frequency, which inherently build different facets** for each sample, increasing feature randomness and diversity during training for better overfitting resistance and generalization.

## QA3: Comparison between SGU and other feature iteration method?

<p><b>Comparison with self-attention mechanism (attn)</b></p>

| T2G Dataset:  | GE⬆️   | CH⬆️   | EY⬆️   | CA⬇️   | HO⬇️   | AD⬆️   | OT⬆️   | HE⬆️   | JA⬆️   | HI⬆️   | FB⬇️   | YE⬇️   | T      | P(M)  |
| :------------- | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :----: | :---: |
| T-MLP          | 0\.706 | 0\.862 | 0\.717 | 0\.449 | 3\.125 | 0\.864 | 0\.814 | 0\.386 | 0\.728 | 0\.729 | 5\.667 | 8\.768 | x1\.00 | 0\.72 |
| T-MLP(attn)    | 0\.708 | 0\.859 | 0\.723 | 0\.452 | 3\.120 | 0\.862 | 0\.806 | 0\.384 | 0\.724 | 0\.728 | 5\.710 | 8\.792 | x1\.68 | 2\.03 |
| T-MLP(3)       | 0\.714 | 0\.866 | 0\.747 | 0\.438 | 3\.063 | 0\.867 | 0\.823 | 0\.386 | 0\.732 | 0\.730 | 5\.629 | 8\.732 | x1\.09 | 2\.16 |
| T-MLP(attn)(3) | 0\.715 | 0\.864 | 0\.767 | 0\.447 | 3\.115 | 0\.867 | 0\.819 | 0\.386 | 0\.730 | 0\.730 | 5\.683 | 8\.773 | x1\.93 | 6\.10 |

**Observations:** As suggested in the previous MLP-based architectures for CV and NLP tasks [12, 25, 54, 55], using self-attention in T-MLP has no significant difference on tabular prediction task performance while increasing training duration and parameter numbers on single T-MLP, and such complexity increasement is more severe when using T-MLP ensemble. A probable explanation is that the simple SGU structure has enough capacity to handle filtered sparse input features, while more complicated attention has no benefit on such sparse features with a risk of introducing noise from the unimportant features.

**Analysis:** Our primary consideration on choosing SGU is to make model lightweight and computation efficient. Here we first analyze the complexity of computation and parameter for SGU and attention mechanism: Given $F$ input features with $d$ hidden size, the time complexity of attention consists of $QK^T$ multiplication (i.e., O($F \times F \times d$)=O($F^2d$)) and $(QK^T)V$ multiplication (i.e., O($F \times d \times F$)=O($F^2d$)), while the one of SGU is equivalent to the later part of attention, i.e., O($F \times d \times F$)=O($F^2d$), saving half of the computational complexity. When it comes to parameter requirement, attention needs O(3d^2) (i.e., $W_Q$, $W_K$, $W_V$), while SGU is O($F^2$). In most architecture studies of tabular model (also in our experiment), $F$ << $d$, thus SGU has a more profound advantage in parameter simplicity. Based on this insight, many pure-MLP works have been explored for efficient architectures in CV and NLP tasks which were on par with or even surpass attention-based Transformer. Besides, gMLP demonstrated performance on NLP tasks is insensitive to replacing self-attention in Transformer with an MLP-based alternative (i.e., SGU) [37].

## QA4: Analysis on why faster than XGBoost?

**For training**, XGBoost always require heavy hyperparameter tuning (HPT), for example, in the experiment of FT-Transformer [23] and T2G-Former [63], XGBoost required 100-iteration HPT, and in the known work of demonstrating GBDTs still outperforms DNNs in typical tabular regime [24], the used SOTA XGBoost performances were obtained after around 400 iterations of HPT. Contrarily, the XGBoost and single-block MLP used in our T-MLP are all kept in fixed hyperparameters, achieving SOTA competitive performances with only one-time training. For inference, since the XGBoost feature selection process is technically converted into PyTorch tensor computation with [Microsoft Hummingbird compiling tools](https://github.com/microsoft/hummingbird), all T-MLP inference process can be accelerated by CUDA operations in an end-to-end manner, while XGBoost still on CPU-GPU hybrid computation. Overall, T-MLP can achieve satisfactory results with faster training and inference than XGBoost


## QA5: How about other baseline ensemble results on SAINT benchmark?

Thank you for your rigorous consideration. Our T-MLP is designed for simplicity and no hyperparameter tuning (HPT) while achieving satisfactory results. On SAINT benchmark, single T-MLP & T-MLP(3) were only trained once, but the SAINT model results were obtained by costly pre-training with downstream HPT, and other strong GBDTs underwent 100-iteration HPT.

Here we additionally compare ensemble results of other DNN baselines with T-MLP(3):

<p><b>Rank (average values and standard deviations) comparison with other DNN ensemble</b></p>

| SAINT Benchmark   | Binclass (9 datasets) | Multiclass (7 datasets) | Regression (10 datasets) |
| :---------------- | :-------------------: | :---------------------: | :----------------------: |
| MLP(3)            | 3\.28(0.67)           | 3\.50(0.87)             | 4\.50(0.58)              |
| TabNet(3)         | 4\.78(0.67)           | 4\.50(0.50)             | 3\.70(1.09)              |
| TabTransformer(3) | 3\.83(0.61)           | 3\.86(1.07)             | 3\.50(0.75)              |
| SAINT(3)          | 1\.50(0.43)           | 1\.64(0.75)             | 1\.65(0.71)              |
| hMLP(3)           | 1\.61(0.65)           | 1\.50(0.50)             | 1\.65(0.78)              |

**Analysis:** An overall trend is that, even without considering pre-training budget of SAINT, T-MLP(3) is still a more cost-effective choice compared to SAINT(3) with negligible performance difference. A core reason of the superiority of T-MLP ensemble compared to other DNN counterparts is its controllable sparsity design in the MLP component, the 3 base MLP models in T-MLP(3) are learned with 3 different fixed learning rates, leading to their distinct and dynamical sparsity structures to increase model diversity and capacity, while other current tabular DNNs (e.g., SAINT, MLP) are using static neural structures, i.e., their architectures cannot be adaptively tailored as feature space or data distribution varies. Actually, the design of ensemble with simple sparse MLPs takes inspiration from GBDT structure, e.g., in XGBoost each CART tree has different pruned tree structure, and our T-MLP emulate such behavior to create GBDT-like simple MLPs.

## QA6: Analysis on the correlation between T-MLP performance and data characteristics?

To further inspect the impact of data characteristics on T-MLP performance, we create pivot tables by filtering datasets with training data volume, numerical feature numbers and categorical feature numbers on T2G-Former benchmark [63] and TabBen benchmark [24].

**For training data volume impact**, we report the average ranks (standard deviations) in different volume ranges on 12 datasets from T2G benchmark as follows, where $N$ is training data volume:

| T2G Benchmark  | $N$<10K (3 datasets) | $N$<50K (5 datasets) | $N$>=50K (4 datasets) |
| :------------- | :----------------: | :----------------: | :-----------------: |
| XGBoost        | 3\.7(1.2)          | 3\.4(3.4)          | 5\.8(3.8)           |
| MLP            | 8\.7(1.5)          | 8\.4(1.7)          | 7\.8(2.6)           |
| SNN            | 7\.0(1.7)          | 8\.6(1.5)          | 8\.8(1.0)           |
| TabNet         | 9\.0(2.6)          | 10\.8(2.2)         | 10\.3(2.9)          |
| DANet-28       | 9\.7(3.2)          | 10\.4(1.9)         | 11\.5(0.6)          |
| NODE           | 8\.0(3.5)          | 8\.4(2.9)          | 4\.4(1.1)           |
| AutoInt        | 10\.3(0.6)         | 7\.8(2.3)          | 6\.9(1.0)           |
| DCNv2          | 9\.7(1.2)          | 7\.2(2.6)          | 8\.8(2.1)           |
| FT-Transformer | 5\.3(1.5)          | 3\.8(2.2)          | 5\.3(3.9)           |
| T2G-Former     | 2\.3(1.5)          | 3\.4(0.9)          | 3\.3(2.6)           |
| T-MLP          | 3\.0(1.0)          | 3\.5(0.7)          | 3\.3(1.0)           |
| T-MLP(3)       | 1\.3(0.6)          | 2\.3(0.3)          | 2\.3(1.0)           |

**Analysis:** The overall trend exhibit a stably consistent superiority of T-MLP(3) in all data volume ranges, with two obvious observations: (1) Single T-MLP (without ensemble) performs better and is more SOTA competitive on large-volume datasets, which is benefited from its DNN properties, while XGBoost begins to fall behind in large datasets; (2) T-MLP benefits more from ensemble operation on small-volume datasets, which is intuitive since small training sets lead to unstable learning results and GBDT-like ensemble can boost both performance and stability.


**For feature type impact**, we report the average ranks (standard deviations) in different categorical rates $\alpha$ (i.e., the proportion of categorical features to the total feature numbers, $\alpha$ = $\frac{C}{F}$, where $C$ is categorical feature amount, and $F$ is the total feature amount) on 16 datasets containing both numerical features and categorical ones from TabBen benchmark as follows:

| TabBen       | **classification** <br> (3 datasets) <br> (0 < $\alpha$ < 0\.5) | **classification** <br> (3 datasets) <br> (0\.5 <= $\alpha$ <= 1) | **regression** <br> (5 datasets) <br> (0 < $\alpha$ < 0\.5) | **regression** <br> (5 datasets) <br> (0\.5 <= $\alpha$ <= 1) |
| :----------- | :-------------------------------------------------- | :---------------------------------------------------- | :---------------------------------------------- | :------------------------------------------------ |
| FT-T         | 5\.7(2.3)                                           | 5\.3(2.5)                                             | 6\.3(1.2)                                       | 7\.3(0.5)                                         |
| ResNet       | 8\.7(0.6)                                           | 7\.0(0.0)                                             | 7\.7(0.5)                                       | 7\.8(0.5)                                         |
| SAINT        | 7\.3(1.2)                                           | 8\.7(0.6)                                             | N/A                                             | N/A                                               |
| GBT          | 5\.0(2.0)                                           | 5\.3(3.1)                                             | 4\.6(0.5)                                       | 4\.4(1.6)                                         |
| HistGBT      | 3\.7(1.5)                                           | 6\.7(2.1)                                             | 4\.3(1.7)                                       | 4\.1(0.3)                                         |
| RandomForest | 5\.3(3.5)                                           | 2\.7(2.3)                                             | 5\.8(2.6)                                       | 5\.9(0.3)                                         |
| XGBoost      | 2\.0(1.7)                                           | 3\.7(0.6)                                             | 1\.6(0.9)                                       | 2\.8(0.5)                                         |
| T-MLP        | 3\.7(2.5)                                           | 3\.3(2.5)                                             | 3\.9(1.0)                                       | 2\.6(1.3)                                         |
| T-MLP(3)     | 3\.3(1.5)                                           | 2\.7(1.2)                                             | 1\.9(0.5)                                       | 1\.3(0.5)                                         |

**Analysis:** According to the pivot results on dataset groups of different categorical rates and tasks, we have three key observations: When tabular datasets contain both categorical and numerical features, (1) the performance of T-MLP is likely to be improved as categorical features dominate the dataset (categorical rates increase), (2) XGBoost begins to fall behind when categorical rates increase, and (3) compared to classification tasks, T-MLP(3) performs more strongly on regression tasks, which may be benefited from its DNN properties, and XGBoost is relatively more powerful when numerical features dominate. Notably, all baseline results in the above table were acquired after hyperparameter tuning of around 400 iterations in the original paper settings, e.g., **XGBoost used around 1.3 hours to search its best configurations on 17-feature "house sales" dataset with 21.6 K samples, while T-MLP(3) only took less than 2 minutes to train. Such difference on cost-effectiveness will be more profound as data scale increases, which is one of our main contributions for carbon-friendly AI**.

<a id="jHCg"></a>

# 💬 To R jHCg
- *2019.06 - 2022.04 (now)*, Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus ornare aliquet ipsum, ac tempus justo dapibus sit amet. 
- *2015.09 - 2019.06*, Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus ornare aliquet ipsum, ac tempus justo dapibus sit amet. 

<a id="LYyH"></a>

# 💬 To R LYyH 

## QA2: Efficiency comparison with GBDT models?
<table style="border-collapse: collapse; border: none; border-spacing: 0px;">
	<caption>
		<b>The overhead of XGBoost training duration against T-MLP</b>
	</caption>
	<tr>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); border-left: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			GE
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			CH
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			EY
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			CA
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			HO
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			AD
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			OT
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			HE
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			JA
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			HI
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			FB
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			YE
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			avg
		</td>
	</tr>
	<tr>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			XGBoost(T)
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); border-left: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x14.72
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x8.32
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x14.05
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x3.87
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x2.75
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x6.13
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x29.89
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x273.80
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x71.17
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x24.13
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x32.85
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x25.42
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x42.26
		</td>
	</tr>
	<tr>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			XGBoost(T*)
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); border-left: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x12.93
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x11.04
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x11.21
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x2.57
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x2.99
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x7.39
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x8.65
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x425.65
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x24.35
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x4.46
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x22.67
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x17.69
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			x45.97
		</td>
	</tr>
</table>

## QA3: The GBDT feature gate has the minimal impact?
<table style="border-collapse: collapse; border: none; border-spacing: 0px;">
	<caption>
		<b>QA3: The detailed ablation on T2G datasets</d>
	</caption>
	<tr>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			T2G Dataset:
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); border-left: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			GE⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			CH⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			EY⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			CA⬇️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			HO⬇️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			AD⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			OT⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			HE⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			JA⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			HI⬆️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			FB⬇️
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			YE⬇️
		</td>
	</tr>
	<tr>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			T-MLP
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-left: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.706</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.862</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.717</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.447</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>3.125</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.864</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.814</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.386</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.728</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>0.729</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>5.667</b>
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			<b>8.768</b>
		</td>
	</tr>
	<tr>
		<td style="border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			w/o sparsity
		</td>
		<td style="border-left: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.681
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.857
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.688
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.450
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			3.136
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.857
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.806
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.377
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.720
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.726
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			5.708
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			8.887
		</td>
	</tr>
	<tr>
		<td style="border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			w/o GBDT FG
		</td>
		<td style="border-left: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.694
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.858
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.692
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.454
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			3.172
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.859
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.809
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.372
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.723
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.728
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			5.736
		</td>
		<td style="text-align: right; padding-right: 3pt; padding-left: 3pt;">
			8.799
		</td>
	</tr>
	<tr>
		<td style="border-right: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			w/o both
		</td>
		<td style="border-left: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.676
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.857
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.673
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.460
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			3.169
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.856
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.803
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.373
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.717
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.724
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			5.759
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			8.896
		</td>
	</tr>
	<tr>
		<td style="border-right: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			T-MLP (Neural FG)
		</td>
		<td style="border-left: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.665
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.858
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.699
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.456
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			3.188
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.852
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.809
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.375
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.721
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.718
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			5.861
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			8.925
		</td>
	</tr>
	<tr>
		<td style="border-right: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			w/o sparsity
		</td>
		<td style="border-left: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.647
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.855
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.675
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.456
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			3.205
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.840
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.804
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.372
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.716
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			0.713
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			5.887
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); text-align: right; padding-right: 3pt; padding-left: 3pt;">
			8.936
		</td>
	</tr>
</table>

## QA4: Insufficient analysis on the impact of GBDT or MLP parameters?
<p align="center">
  <img src="img/xgb-hp-analysis.png" alt="sym" width="550">
    <figcaption style="text-align: center;">The imapct of decision tree count in XGBoost of T-MLP</figcaption>
</p>

<b>Analysis: The impact of CART tree amount variation in XGBoost of T-MLP</b> on 2 classificaiton (GE & JA) and 2 regression (CA & FB) datasets. <b>In the paper we uniformly assigned the tree amount as 2,000 as the default XGBoost settings in [23]</b>, and we gradually reduce this value to get such performance variation figure. The results on CA datasets are multiplied by 10. There are several observations:

- Each datasets have different appetite on the best tree amount of the GBDT.

- The default GBDT configs from [23] tends to overfit the data since T-MLP on all four datasets can have a better score with reduced tree amount.

- The slight modification on the default tree amount (i.e., 2,000) does not significantly affect the T-MLP performance.

We will include more fine-grained parameter impact illustrations in the final version.

## Detail 1～4
<b>Detail 1:</b> The statement "slight hyperparameter modification will not change the overall feature preference trend" is not convincing?

- A: Thank you for your rigorous consideration. The additionally conducted experiment in the above QA4 is partially for this detail question, while there exist other parameters of GBDTs, we will add more fine-grained GBDT parameter analysis in the final version. 

<b>Detail 2:</b> Full efficiency comparison with GBDTs should be performed?

- A: We agree with your suggestion, and the table of QA2 has partially address this question, we are going to add efficiency comparison of other GBDTs (i.e., CatBoost, LightGBM) in other benchmarks in the final version.

<b>Detail 3:</b> Explanation on why no need for hyperparameter tuning but such great results?

- A: The superiority of the T-MLP framework comes from 3 folds and we will include them finally: 
	- (1) Throughout GBDT-level sample-wise feature selection: It has been widely observed emulating the feature selection behavior of GBDTs helps tabular prediction (e.g., TabNet [3], LSPNN [64]), while the previous attempt focus on the neural-based soft emulation, which effectiveness is affected by the overall neural networks. Our T-MLP faithfully use and train real GBDTs with decoupled training process, i.e., the GBDTs are trained first, then DNN parts, which will not affect the selection ability.
	- (2) Sparse neural structure: Inspired by GBDT pruned structure and evidenced by recent works (e.g., TabCaps [13], LSPNN [64]), introducing sparsity to tree-like linearly connected neural models helps generalization.
	- (3) NAS during training: An implicit structure hyperparameter tuning is done during one-time training, i.e., searching the best sparse structure can be regarded as a parameter optimization process. Moreover, based on the simple but sparse MLP architectures, the ensemble operation can be effectively done without different data splits for each MLP branch, directly using different learning rates will produce distinct sparse structures to expand the sparse assumption space.

<b>Detail 4:</b> Lack feature engineering experiments?

- A: In this paper all baselines were conducted with uniform common feature preprocessing for fair comparison. We are willing to open a section for feature engineering experiments in the final version.

<a id="hswh"></a>

# 💬 To R hswh

## Default hyperparameters (HPs) of T-MLP in this paper
<table style="border-collapse: collapse; border: none; border-spacing: 0px;">
	<tr>
		<td colspan="2" style="border-bottom: 1px solid rgb(0, 0, 0); border-top: 1px solid rgb(0, 0, 0); text-align: center; padding-right: 3pt; padding-left: 3pt;">
			T-MLP's GBDT architecture: XGBoost
		</td>
	</tr>
	<tr>
		<td style="border-top: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			Model HPs
		</td>
		<td rowspan="2" style="border-left: 1px solid windowtext; border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			Same as the default XGBoost configs used in the Table 4 of FT-T paper [23], you can find and download the HP config file from its <a href="https://github.com/yandex-research/rtdl-revisiting-models/blob/main/output/adult/xgboost/default/0/stats.json"><u>repo</u></a>, other unmentioned HPs are kept default as <a href="https://xgboost.readthedocs.io/en/stable/python/python_api.html#module-xgboost.sklearn"><u>XGBoost official APIs</u></a>.
		</td>
	</tr>
	<tr>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			Training HPs
		</td>
	</tr>
	<tr>
		<td colspan="2" style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: center; padding-right: 3pt; padding-left: 3pt;">
			T-MLP's DNN architecture: MLP
		</td>
	</tr>
	<tr>
		<td colspan="2" style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: center; padding-right: 3pt; padding-left: 3pt;">
			Model HPs
		</td>
	</tr>
	<tr>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			Hidden size
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-left: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			1024; decided by keeping equivalent storage space as the MLP baselines in [23]
		</td>
	</tr>
	<tr>
		<td style="border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			Intermediate factor
		</td>
		<td style="border-left: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			2/3, i.e., with an intermediate size of 1024 x 2/3 = 676; refer to the one in FT-T [23]
		</td>
	</tr>
	<tr>
		<td style="border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			Residual dropout
		</td>
		<td style="border-left: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			0.1; refer to the one in FT-T [23]
		</td>
	</tr>
	<tr>
		<td style="border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			Layer count
		</td>
		<td style="border-left: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			1
		</td>
	</tr>
	<tr>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			Sparsity rate
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-left: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			0.33, the only HP for controlled pruning algorithm referring to CoFi [62]
		</td>
	</tr>
	<tr>
		<td colspan="2" style="border-top: 1px solid rgb(0, 0, 0); border-bottom: 1px solid rgb(0, 0, 0); text-align: center; padding-right: 3pt; padding-left: 3pt;">
			Training HPs
		</td>
	</tr>
	<tr>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			Learning rate
		</td>
		<td style="border-top: 1px solid rgb(0, 0, 0); border-left: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			(A)&nbsp;&nbsp; For single T-MLP, 1e-4; (B) For ensemble version, i.e., T-MLP(3), using 1e-4, 5e-4, 1e-3 for three branches respectively; refer to [23]
		</td>
	</tr>
	<tr>
		<td style="border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			Weight decay
		</td>
		<td style="border-left: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			0
		</td>
	</tr>
	<tr>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-right: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			Optimizer
		</td>
		<td style="border-bottom: 1px solid rgb(0, 0, 0); border-left: 1px solid rgb(0, 0, 0); padding-right: 3pt; padding-left: 3pt;">
			AdamW, with all other training HPs kept default
		</td>
	</tr>
</table>