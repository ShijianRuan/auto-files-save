|  |  |
| --- | --- |
| **项目名称/Project Name** | **Fenix** |
| **产品名称/Product Name** | **uOmnispace.MI** |

|  |
| --- |
| **MI算法设计规范/MI Algorithm Design Specification**  88000968-CDS-AII-02  生效日期/Valid from: **See Agile** |

© 联影医疗 版权所有

© United Imaging Healthcare Reserved

**更改记录/History**

**目录/Table of Contents**

[更改记录/History 2](#_Toc218763039)

[目录/Table of Contents 3](#_Toc218763040)

[1 介绍/Introduction 5](#_Toc218763041)

[1.1 目的/Purpose 5](#_Toc218763042)

[1.2 范围/Scope 5](#_Toc218763043)

[1.3 定义和缩略语/Definitions and Abbreviations 5](#_Toc218763044)

[1.3.1 定义/Definitions 5](#_Toc218763045)

[1.3.2 缩略语/Abbreviations 5](#_Toc218763046)

[1.4 参考文件/References 5](#_Toc218763047)

[2 概要/General Description 6](#_Toc218763048)

[2.1 设计约束/Design Constraints 6](#_Toc218763049)

[2.2 技术概述/Technical Overview 6](#_Toc218763050)

[3 数据集设计规范/ Design Specification of Data Set 7](#_Toc218763051)

[4 算法设计/ Algorithm Design 8](#_Toc218763052)

[4.1 算法清单/Algorithm List 8](#_Toc218763053)

[4.2 多模态肿瘤追踪应用相关算法/MM Oncology Related Algorithms 8](#_Toc218763054)

[4.2.1 CT器官分割算法/CT Organ Segmentation Algorithm 8](#_Toc218763055)

[4.2.2 MR器官分割算法/MR Organ Segmentation Algorithm 16](#_Toc218763056)

[5 风险控制措施的设计/The Design of the Risk Control Method 25](#_Toc218763057)

[6 网络安全的设计/The Design of the Cybersecurity 26](#_Toc218763058)

[7 基本质量属性/General Quality Feature 27](#_Toc218763059)

[7.1 可测性/Testability 27](#_Toc218763060)

[7.2 可扩展性考虑分析/Scalability and Extensibility 27](#_Toc218763061)

[7.3 可维护性/Maintainability 27](#_Toc218763062)

[7.4 可适用性/Adaptability 27](#_Toc218763063)

[8 安装和服务/Installation & Service 28](#_Toc218763064)

[9 终止实现的设计/Terminated Design 29](#_Toc218763065)

[10 未决事项/Open Issues 30](#_Toc218763066)

[设计列表/Table of Design Keys 31](#_Toc218763067)

图表索引

[图 1 CT器官分割算法流程图 8](#_Toc218674751)

[图 2 CT器官分割结果示意图 11](#_Toc218674752)

[图 3 MR器官分割算法流程图 18](#_Toc218674753)

[图 4 MR器官分割结果示意图 21](#_Toc218674754)

[Figure 1 Flow Chart of the CT Organ Segmentation Algorithm 9](#_Toc218674755)

[Figure 2 Diagram of CT organ segmentation result 11](#_Toc218674756)

[Figure 3 Flow Chart of the MR Organ Segmentation Algorithm 18](#_Toc218674757)

[Figure 4 Diagram of MR organ segmentation result 21](#_Toc218674758)

# 介绍/Introduction

## 目的/Purpose

本文件描述了uOmnispace.MI相关算法的设计规范。

This document describes the design specifications of the relevant algorithms in uOmnispace.MI.

## 范围/Scope

本文档适用于以下应用：多模态肿瘤追踪应用。

This document is intended for the following applications: MM Oncology application.

## 定义和缩略语/Definitions and Abbreviations

### 定义/Definitions

N.A.

### 缩略语/Abbreviations

|  |  |  |
| --- | --- | --- |
| CT | Computed Tomography | 电子计算机断层扫描 |
| MR | Magnetic Resonance | 磁共振成像 |

## 参考文件/References

[1]. 88000968-DAF-MIA 数据收集规范/ Data Gathering Specification

[2]. 88000968-SFS-MIP 系统功能规范/System Functional Specification

# 概要/General Description

在算法开发设计时，应考虑以下因素，从而来确保软件算法的安全性和有效性：

代码的编写符合C++编程规范；

有合理的错误处理机制，避免算法错误的执行；

选择成熟的算法，从而减少潜在的安全缺陷；

此外，算法也会通过设计评审、代码评审、代码单元测试以及算法测试等多个活动，来确保算法的安全性和有效性。

When developing and designing algorithms, the following factors should be considered to ensure the security and effectiveness of software algorithms:

The code is written in accordance with the C++ programming standard;

There is a reasonable error handling mechanism to avoid the execution of algorithm errors;

Choose mature algorithms to reduce potential security vulnerabilities;

In addition, algorithms will ensure their security and effectiveness through multiple activities such as design review, code review, code unit testing, and algorithm testing.

## 设计约束/Design Constraints

本文档所述算法中，运用深度学习算法的需在搭载Nvidia GTX 1060图形处理器的计算机硬件环境下运行，软件环境需要匹配的CUDA、CUDNN版本。

The algorithms described in this document, the use of deep learning algorithms need to run in the computer hardware environment equipped with Nvidia GTX 1060 graphics processor, the software environment needs to match CUDA, CUDNN versions.

## 技术概述/Technical Overview

本文档所述算法在研发过程中神经网络的训练以及测试基于Pytorch框架。

The training and testing of neural networks in the development process of the algorithms described in this document are based on the Pytorch framework.

# 数据集设计规范/ Design Specification of Data Set

请参考数据收集规范[1]。

# 算法设计/ Algorithm Design

## 算法清单/Algorithm List

|  |  |
| --- | --- |
| 算法名称 | 功能描述 |
| CT 器官分割算法/CT Organ Segmentation Algorithm | 针对CT数据，分割出器官区域  Segment the organ regions from the CT data. |
| MR器官分割算法/MR Organ Segmentation Algorithm | 针对MR数据，分割出器官区域  Segment the organ regions from the MR data. |

## 多模态肿瘤追踪应用相关算法/MM Oncology Related Algorithms

### CT器官分割算法/CT Organ Segmentation Algorithm

#### 功能设计/Functional Design

#### 设计视图/Design Viewpoint

##### 算法流程图/ Flow Chart

![](images/fb083a5ee50a.png)

图 1 CT器官分割算法流程图

![](images/f8fe87f4efde.png)

Figure 1 Flow Chart of the CT Organ Segmentation Algorithm

##### 其它设计视图

N.A.

#### 接口设计/Interface Design

algo-intelliworkflow/Interface/McsfAlgoImageRecognitionInterface.h

// Supported modality types

enum Modality {

CT,

MR

};

// Supported organ list for CT segmentation

static const std::unordered\_set<std::string> CT\_ORGAN\_LIST = { "all", "spleen", "kidney", "gallbladder","liver", "stomach", "pancreas", "adrenal\_gland", "lung", "esophagus", "trachea", "thyroid\_gland", "small\_bowel", "duodenum", "colon", "urinary\_bladder", "prostate", "sacrum", "vertebrae", "heart", "aorta", "pulmonary\_vein", "brachiocephalic\_trunk", "subclavian\_artery","common\_carotid\_artery", "brachiocephalic\_vein", atrial\_appendage\_left", superior\_vena\_cava","inferior\_vena\_cava", "portal\_vein\_and\_splenic\_vein", "iliac\_artery", "iliac\_vena", "humerus","scapula", "clavicula", "femur", "hip", "spinal\_cord", "gluteus\_maximus", "gluteus\_medius", "gluteus\_minimus", "autochthon", "iliopsoas", "brain", "skull", "rib", "sternum", "costal\_cartilages", "breast", "parotid\_gland", "submandibular\_gland", "uterus"

};

// Supported Segmentation Organs

enum Seg\_obj {

ORGANS,

BONES,

ORGANS\_fast,

ORGANS\_MUSCLE,

ORGANS\_MMOncology,

CHAMBER

};

// brief 要求数据必须为LPS方向，进行全量器官分割

// param[in] patient\_info: 包含分割任务的结构体（模态+器官列表），支持输入"all"进行全部分割

// param[in] psData: 要分割的3D数据。要求输入必须为LPS格式的图像，dicom输入时需输入图像的Hu值

// param[in] iDim: 分割数据的尺寸，iDim[0]为x轴长度，iDim[1]为y轴长度，iDim[2]为z轴长度

// param[in] dSpacing: 分割数据的spacing，方向与iDim相同

// param[out] puMask: 获取的分割结果

// param[in] pProgress: 进度条

// param[in] pBedMask: 去床板结果，仅在CT肋骨分割模型中使用。其他场景可给nullptr。

// return 成功返回true，失败返回false

bool AutoWholeBodySegment\_Kunpeng\_Seg(Modality modality,

const std::unordered\_set<std::string>& organsToSegment,

short\* psData,

int\* iDim,

double\* dSpacing,

unsigned char\* puMask,

IProgress\* pProgress,

unsigned char\* pBedMask = nullptr);

#### 算法设计/Algorithm Design

##### 网络训练阶段/Network Training Stage

第一：图像预处理

对训练数据进行预处理，即统一图像分辨率至[1.5,1.5,1.5]（单位毫米），然后随机裁剪128\*128\*128尺寸，裁剪图像归一化到[-1,1]。对训练数据进行数据增广，进行x、y、z三个方向的50%概率随机翻转。进行x、y、z三个方向[-15°,15°]范围内随机角度旋转。图像按照[0.85,1.25]范围内随机比例缩放。

第二：网络训练

数据集输入Unet分割网络训练，执行网络模型训练，待损失函数收敛，器官分割误差Dice系数均趋于稳定时，停止模型训练，并将网络进行部署。

Step1：Image preprocessing

Preprocess the training data by unifying the image resolution to [1.5,1.5,1.5] (millimeter), then randomly crop the image to a size of 128\*128\*128. The cropped image was normalized to [-1,1]. Augment training data randomly by flipping the images in the direction of x, y, and z with 50% probability, rotating the images at random angles with the range of [-15°,15°] in the x, y, and z, and scaling the images with the range of [0.85,1.25].

Step2: Network training

Train the segmentation network model (UNet) on the training dataset. When the loss function is converged and the Dice coefficients of organ segmentation error tend to stabilize, stop the model training.

##### 部署测试阶段/Deployment Test Stage

第一：图像预处理

图像被统一到spacing[1.5, 1.5, 1.5] （单位毫米）,然后裁剪到128\*128\*128尺寸。根据输入图像像素的0均值，1标准差归一化图像。

Step1：Image preprocessing

The image is unified to spacing [1.5, 1.5, 1.5], and then cut to 128\*128\*128 size. Normalized image based on 0-mean and 1-standard deviation of input image pixels.

第二：图像分割

使用Unet网络完成器官分割。包含器官区域和背景。如图4.2.1-2所示。

Step2: Image segmentation

Use the Unet network to complete the segmentation of the organs, which includes the organ regions, and the background, as shown in Figure 4.2.1-2.

![](images/bb24191691c2.png)

图 2 CT器官分割结果示意图

Figure 2 Diagram of CT organ segmentation result

第三：将分割结果还原成原始输入尺寸

将分割结果还原到原始输入图像的spacing 和大小。

Step3: Resize the segmentation result to the original input size

The segmentation results are restored to the spacing and size of the original input image.

#### 算法性能的设计要求/Design Spec of Algorithm Performance

DICE系数是验证医学图像分割最常用的指标。因此，我们将使用DICE来衡量我们的分割算法。DICE定义如下：

DICE = ![](images/1238e74e612d.x-wmf)

其中G代表金标准，T代表分割结果

The DICE coefficient is the most commonly used metric for validating medical image segmentation. Therefore, we will use the DICE coefficient to evaluate our segmentation algorithm. The DICE coefficient is defined as follows:

DICE = ![](images/3c0e8fc8e32f.x-wmf)

where G represents the ground truth and T represents the segmentation result.

根据友商测试指标[1-8]和多个文献[9-14]的DICE结果，按照大于等于平均水平的原则设置通过标准，具体如下表。如果器官分割的平均DICE大于对应的通过标准，则证明算法是有效的。

Based on the test metrics of competitors [1-8] and DICE results from multiple literature sources [9-14], the passing criteria are established following the principle of being greater than or equal to the average level, as detailed in the table below. If the average DICE score for organ segmentation exceeds the corresponding passing criterion, the algorithm is proven to be effective.

|  |  |  |  |
| --- | --- | --- | --- |
| **部位/Part** | **器官/Organ** | **子结构/Substructure** | **通过标准/**  **passing criterion** |
| 头颈/  Head&Neck | 大脑/Brain |  | 0.975 |
| 甲状腺/Thyroid |  | 0.800 |
| 胸部/Thorax | 主动脉/Aorta |  | 0.900 |
| 心脏/Heart |  | 0.930 |
| 肺/Lung | Lung\_L Lung\_R | 0.980 0.980 |
| 上腔静脉/Superior Vena Cava |  | 0.900 |
| 腹部/Abdomen | 肾上腺/Adrenal | Adrenal\_L Adrenal\_R | 0.850  0.850 |
| 十二指肠/Duodenum |  | 0.850 |
| 胆囊/ Gallbladder |  | 0.870 |
| 肾/Kidney | Kidney\_L Kidney\_R | 0.940 0.940 |
| 肝脏/Liver |  | 0.960 |
| 胰腺/Pancreas |  | 0.850 |
| 小肠/Small Intestine |  | 0.900 |
| 脾/Spleen |  | 0.950 |
| 胃/Stomach |  | 0.900 |
| 盆腔/ Pelvis | 膀胱/Bladder |  | 0.930 |
| 前列腺/Prostate |  | 0.880 |
| 骨骼/Skeleton | 锁骨/Clavicula | Clavicula\_L Clavicula\_R | 0.920 0.920 |
| 股骨/Femur | Femur\_L Femur\_R | 0.960 0.960 |
| 髋关节/Hip | Hip\_L Hip\_R | 0.950 |
| 肱骨/Humerus | Humerus\_L Humerus\_R | 0.950 0.950 |
| 胸骨/Sternum |  | 0.920 |
| 骶骨/Sacrum |  | 0.920 |
| 肩胛骨/Scapula | Scapula\_L Scapula\_R | 0.970  0.970 |
| 头骨/Skull |  | 0.970 |
| 脊髓/Spinal Cord |  | 0.900 |
| 肋骨/Rib |  | 0.850 |
| 椎骨/Vertebrae |  | 0.900 |
| 全身骨/Bone in Whole Body |  | 0.850 |
| 肌肉/Muscle | 竖脊肌/Erector Spinae | Erector\_L Erector\_R | 0.950 0.950 |
| 臀大肌/GluteusMax | GluteusMax\_L GluteusMax\_R | 0.960 0.960 |
| 臀中肌/GluteusMed | GluteusMed\_L GluteusMed\_R | 0.960 0.960 |
| 臀小肌/GluteusMin | GluteusMin\_L GluteusMin\_R | 0.950 0.950 |
| 髂腰肌/Iliopsoas | Iliopsoas\_L Iliopsoas\_R | 0.930 0.930 |

Note:

* L / R: 左侧/右侧 (Left / Right)，例如 Lung\_L 为左肺，Lung\_R 为右肺。
* 肌肉名称后缀 (Max, Med, Min): 最大 / 中 / 最小 (Maximus / Medius / Minimus)，例如 GluteusMax 为臀大肌，GluteusMed 为臀中肌，GluteusMin 为臀小肌。

Note:

* L / R: Left / Right, e.g., Lung\_L is left lung, Lung\_R is right lung.
* Muscle suffix (Max, Med, Min): Maximus / Medius / Minimus, e.g., GluteusMax is gluteus maximus, GluteusMed is gluteus medius, GluteusMin is gluteus minimus.

**参考文献/reference：**

[1] U.S. Food & Drug Administration. 510(k) Premarket Notification - K230082: GE Healthcare, Auto Segmentation (CT). Silver Spring, MD: FDA; 2023. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfPMN/pmn.cfm?ID=K230082

[2] U.S. Food & Drug Administration. 510(k) Premarket Notification - K213976: MIM Software, Contour ProtégéAI (CT/MR). Silver Spring, MD: FDA; 2021. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfPMN/pmn.cfm?ID=K213976

[3] U.S. Food & Drug Administration. 510(k) Premarket Notification - K242745: Siemens Healthineers, AI-Rad Companion Organs RT (CT/MR). Silver Spring, MD: FDA; 2024. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfpmn/pmn.cfm?ID=K242745

[4] U.S. Food & Drug Administration. 510(k) Premarket Notification - K232899: Radformation, AutoContour (Model RADAC V4, CT/MR). Silver Spring, MD: FDA; 2023. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfpmn/pmn.cfm?ID=K232899

[5] U.S. Food & Drug Administration. 510(k) Premarket Notification - K242729: Radformation, AutoContour (Model RADAC V3, CT/MR). Silver Spring, MD: FDA; 2024. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfpmn/pmn.cfm?ID=K242729

[6] U.S. Food & Drug Administration. 510(k) Premarket Notification - K230685: Radformation, AutoContour (Model RADAC V2). Silver Spring, MD: FDA; 2023. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfpmn/pmn.cfm?ID=K230685

[7] U.S. Food & Drug Administration. 510(k) Premarket Notification - K220598: Radformation, AutoContour (Model RADAC V2). Silver Spring, MD: FDA; 2022. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfpmn/pmn.cfm?ID=K220598

[8] U.S. Food & Drug Administration. 510(k) Premarket Notification - K232928: Wisdom Technologies, DeepContour (V1.0, CT). Silver Spring, MD: FDA; 2023. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfPMN/pmn.cfm?ID=K232928

[9] Wasserthal J, Breit HC, Meyer MT, et al. TotalSegmentator: Robust segmentation of 104 anatomic structures in CT images. Radiol Artif Intell. 2023;5(5):e230024. doi:10.1148/ryai.230024

[10] Wu D, Zhi X, Liu X, et al. Utility of a novel integrated deep convolutional neural network for the segmentation of hip joint from computed tomography images in the preoperative planning of total hip arthroplasty. J Orthop Surg Res. 2022;17(1):164. doi:10.1186/s13018-022-02932-w

[11] Satir OB, Eghbali P, Becce F, et al. Automatic quantification of scapular and glenoid morphology from CT scans using deep learning. Eur J Radiol. 2024;177:111588. doi:10.1016/j.ejrad.2024.111588

[12] Kreher R, Hinnerichs M, Preim B, Saalfeld S, Surov A. Deep-learning-based segmentation of skeletal muscle mass in routine abdominal CT scans. In Vivo. 2022;36(4):1807-1811. doi:10.21873/invivo.12896

[13] Kim HS, Kim H, Kim S, et al. Precise individual muscle segmentation in whole thigh CT scans for sarcopenia assessment using U-net transformer. Sci Rep. 2024;14(1):3301. doi:10.1038/s41598-024-53707-8

[14] Gillot M, Baquero B, Le C, et al. Automatic multi-anatomical skull structure segmentation of cone-beam computed tomography scans using 3D UNETR. PLoS One. 2022;17(10):e0275033. doi:10.1371/journal.pone.0275033

|  |  |
| --- | --- |
| 训练/调优评价标准：  Training/tuning evaluation criterion | 采用医学图像分割方法中常用的DICE评价指标[1]作为Loss函数。如果所选模型符合以下评价标准，则认为所选模型合格：   1. 训练集中Loss曲线达到收敛，相邻两次Loss迭代之差小于10-1。 2. 将模型在调优集的评价标准设置为：器官的DICE的平均值大于对应的通过标准。   The commonly used DICE evaluation metric [1] for medical image segmentation methods is used as the loss function. If the selected model meets the following evaluation criteria, it is considered qualified:   1. The loss curve in the training set converges, with a difference of less than 10-1 between the loss iterations. 2. The model's evaluation criterion in the tuning set is set as the average DICE score for the organs being greater than corresponding passing criteria.   Reference  [1] Wong K C L , Moradi M , Tang H , et al. 3D Segmentation with Exponential Logarithmic Loss for Highly Unbalanced Object Sizes[C]// International Conference on Medical Image Computing and Computer-Assisted Intervention. Springer, Cham, 2018. |

#### 设计限制/Design Limitation

对于CT器官分割，以下情况中分割结果可能不佳：

1.非标准的解剖结构(如先天性畸形、手术后改变等)或病变区域(如肿瘤、炎症等)

* 解剖变异与先天性异常：例如器官缺如/发育不全（单侧肾缺失）、器官融合（马蹄肾）、异位或骨骼系统变异，可能导致模型无法识别或错误分割。
* 术后改变与植入物：例如器官切除后，模型可能在原始位置生成假阳性分割；器官移植后位置改变、外科重建或植入物（特别是金属假体）造成的伪影，均可能导致分割错误。
* 广泛的病理改变：例如巨大的占位性病变（大肿瘤）可能导致器官体积被严重高估或轮廓无法识别；弥漫性实质病变（晚期肝硬化、重度脂肪肝）会显著降低边界准确性；大量积液/积气或肠管扩张会推移并扭曲邻近器官。

2.低对比度或噪声严重的图像

* 伪影与噪声：严重的运动伪影、线束硬化伪影或高图像噪声会破坏纹理和形态细节，可能导致分割不连续或碎裂。
* 低分辨率或大层厚：会丢失精细的解剖细节，尤其影响小器官（如肾上腺、胆囊）的边界精确描绘。
* 低剂量CT扫描：固有的高噪声和低对比噪声比会使器官边界模糊，对于小器官或本身对比度低的结构（如胰腺与周围脂肪），可能导致分割出现空洞、边界不规则或完全漏检。

3.患者年龄小于20岁

For CT organ segmentation, the segmentation results may exhibit reduced accuracy in the following scenarios:

1.Non-standard anatomical structures (e.g., congenital anomalies, post-surgical alterations) or pathological regions (such as tumors, inflammation, etc.).

* Anatomical Variants & Congenital Anomalies: e.g., organ agenesis/hypoplasia (unilateral renal agenesis), organ fusion (horseshoe kidney), ectopic locations, or skeletal system variants, which may cause the model to fail recognition or produce erroneous segmentations.
* Post-Surgical Changes & Implants: e.g., after organ resection, the model may generate false-positive segmentations at the native location; altered organ position post-transplantation, surgical reconstruction, or implants (especially metallic prostheses causing artifacts) can all lead to segmentation errors.
* Extensive Pathological Changes: e.g., large space-occupying lesions (massive tumors) may cause severe overestimation of organ volume or complete failure to recognize its contour; diffuse parenchymal diseases (advanced cirrhosis, severe hepatic steatosis) significantly reduce boundary accuracy; massive effusion/pneumatosis or bowel distension can displace and deform adjacent organs.

2.Images with low contrast or severe noise.

* Artifacts & Noise: Severe motion artifacts, beam hardening artifacts, or high image noise degrade texture and morphological details, potentially resulting in discontinuous or fragmented segmentations.
* Low Resolution or Large Slice Thickness: Loss of fine anatomical details, particularly affecting accurate boundary delineation of small organs (e.g., adrenal glands, gallbladder).
* Low-Dose CT Scans: Inherently higher noise and lower contrast-to-noise ratio blur organ boundaries. For small organs or structures with inherently low contrast (e.g., pancreatic border), this may cause holes, irregular boundaries, or complete missed detections.

3. Patients under the age of 20.

### MR器官分割算法/MR Organ Segmentation Algorithm

#### 功能设计/Functional Design

#### 设计视图/Design Viewpoint

##### 算法流程图/ Flow Chart

![](images/0fb1c2e33da9.png)

图 3 MR器官分割算法流程图

![](images/892f55ded7fd.png)

Figure 3 Flow Chart of the MR Organ Segmentation Algorithm

##### 其它设计视图

N.A.

#### 接口设计/Interface Design

algo-intelliworkflow/Interface/McsfAlgoImageRecognitionInterface.h

// Supported modality types

enum Modality {

CT,

MR

};

// Supported organ list for MR segmentation

static const std::unordered\_set<std::string> MR\_ORGAN\_LIST = { "spleen", "kidney", "gallbladder", "liver", "stomach", "pancreas", "adrenal\_gland", "lung", "esophagus", "small\_bowel", "duodenum", "colon", "urinary\_bladder", "prostate", "sacrum", "vertebrae", "intervertebral\_discs", "spinal\_cord", "heart", "aorta", "inferior\_vena\_cava", "portal\_vein\_and\_splenic\_vein", "iliac\_artery", "iliac\_vena", "humerus", "scapula", "clavicula", "femur", "hip", "gluteus\_maximus", "gluteus\_medius", "gluteus\_minimus", "autochthon", "iliopsoas", "brain"

};

// Supported Segmentation Organs

enum Seg\_obj {

ORGANS,

BONES,

ORGANS\_fast,

ORGANS\_MUSCLE,

ORGANS\_MMOncology,

CHAMBER

};

// brief 要求数据必须为LPS方向，进行全量器官分割

// param[in] Modality\_seg: 分割任务模态

// param[in] organsToSegment: 要分割的器官列表

// param[in] psData: 要分割的3D数据。要求输入必须为LPS格式的图像

// param[in] iDim: 分割数据的尺寸，iDim[0]为x轴长度，iDim[1]为y轴长度，iDim[2]为z轴长度

// param[in] dSpacing: 分割数据的spacing，方向与iDim相同

// param[out] puMask: 获取的分割结果

// param[in] pProgress: 进度条

// param[in] pBedMask: 去床板结果，仅在CT肋骨分割模型中使用。其他场景可给nullptr。

// return 成功返回true，失败返回false

bool AutoWholeBodySegment\_Kunpeng\_Seg(Modality Modality\_seg,

const std::unordered\_set<std::string>& organsToSegment,

short\* psData,

int\* iDim,

double\* dSpacing,

unsigned char\* puMask,

IProgress\* pProgress,

unsigned char\* pBedMask = nullptr);

bool \_MCSF\_ALGO\_INTELLIWORKFLOW\_Interface\_API AutoWholeBodySegment\_Kunpeng\_Seg(Modality Modality\_seg, const std::unordered\_set<std::string>& organsToSegment, short\* psData, int\* iDim, double\* dSpacing, unsigned char\* puMask, IProgress \*pProgress, unsigned char\* pBedMask = nullptr);

#### 算法设计/Algorithm Design

##### 网络训练阶段/Network Training Stage

第一：图像预处理

对训练数据进行预处理，即统一图像分辨率至[1.5,1.5,1.5]（单位毫米），然后随机裁剪128\*128\*128尺寸，裁剪图像归一化到[-1,1]。对训练数据进行数据增广，进行x、y、z三个方向的50%概率随机翻转。进行x、y、z三个方向[-15°,15°]范围内随机角度旋转。图像按照[0.85,1.25]范围内随机比例缩放。

第二：网络训练

数据集输入Unet分割网络训练，执行网络模型训练，待损失函数收敛，器官分割误差Dice系数均趋于稳定时，停止模型训练，并将网络进行部署。

Step1：Image preprocessing

Preprocess the training data by unifying the image resolution to [1.5,1.5,1.5] (millimeter), then randomly crop the image to a size of 128\*128\*128. The cropped image was normalized to [-1,1]. Augment training data randomly by flipping the images in the direction of x, y, and z with 50% probability, rotating the images at random angles with the range of [-15°,15°] in the x, y, and z, and scaling the images with the range of [0.85,1.25].

Step2: Network training

Train the segmentation network model (UNet) on the training dataset. When the loss function is converged and the Dice coefficients of organ segmentation error tend to stabilize, stop the model training.

##### 部署测试阶段/Deployment Test Stage

第一：图像预处理

图像被统一到spacing[1.5, 1.5, 1.5] （单位毫米）,然后裁剪到128\*128\*128尺寸。根据输入图像像素的0均值，1标准差归一化图像。

Step1：Image preprocessing

The image is unified to spacing [1.5, 1.5, 1.5], and then cut to 128\*128\*128 size. Normalized image based on 0-mean and 1-standard deviation of input image pixels.

第二：图像分割

使用Unet网络完成器官分割。包含器官区域和背景。如图4.2.2-4所示。

Step2: Image segmentation

Use the Unet network to complete the segmentation of the organs, which includes the organ regions, and the background, as shown in Figure 4.2.2-4.

![](images/6554693623e1.png)

图 4 MR器官分割结果示意图

Figure 4 Diagram of MR organ segmentation result

第三：将分割结果还原成原始输入尺寸

将分割结果还原到原始输入图像的spacing 和大小。

Step3: Resize the segmentation result to the original input size

The segmentation results are restored to the spacing and size of the original input image.

#### 算法性能的设计要求/Design Spec of Algorithm Performance

DICE系数是验证医学图像分割最常用的指标。因此，我们将使用DICE来衡量我们的分割算法。DICE定义如下：

DICE = ![](images/3d3bc9b9a0d2.x-wmf)

其中G代表金标准，T代表分割结果

The DICE coefficient is the most commonly used metric for validating medical image segmentation. Therefore, we will use the DICE coefficient to evaluate our segmentation algorithm. The DICE coefficient is defined as follows:

DICE = ![](images/682d48ee18dd.x-wmf)

where G represents the ground truth and T represents the segmentation result.

根据友商测试指标[1-8]和多个文献[9-22]的DICE结果，按照大于等于平均水平的原则设置通过标准，具体如下表。如果器官分割的平均DICE大于对应的通过标准，则证明算法是有效的。

Based on the test metrics of competitors [1-8] and DICE results from multiple literature sources [9-22], the passing criteria are established following the principle of being greater than or equal to the average level, as detailed in the table below. If the average DICE score for organ segmentation exceeds the corresponding passing criterion, the algorithm is proven to be effective.

|  |  |  |  |
| --- | --- | --- | --- |
| **部位/Part** | **器官/Organ** | **子结构/Substructure** | **通过标准/**  **passing criterion** |
| 头颈/  Head&Neck | 大脑/Brain |  | 0.980 |
| Thorax  胸部/Thorax | 主动脉/Aorta |  | 0.950 |
| 心脏/Heart |  | 0.900 |
| 肺/Lung | Lung\_L Lung\_R | 0.960  0.960 |
| 腹部/Abdomen | 十二指肠/Duodenum |  | 0.700 |
| 肾/Kidney | Kidney\_L Kidney\_R | 0.930  0.940 |
| 肝脏/Liver |  | 0.950 |
| 脾/Spleen |  | 0.940 |
| 胃/Stomach |  | 0.880 |
| 盆腔/ Pelvis | 膀胱/Bladder |  | 0.930 |
| 前列腺/Prostate |  | 0.830 |
| 股骨/Femur | Femur\_L Femur\_R | 0.850 0.900 |
| 脊髓/Spinal Cord |  | 0.880 |
| 肌肉/Muscle | 竖脊肌/Erector Spinae | Erector\_L Erector\_R | 0.930  0.930 |
| 臀大肌/GluteusMax | GluteusMax\_L GluteusMax\_R | 0.930  0.930 |
| 臀中肌/GluteusMed | GluteusMed\_L GluteusMed\_R | 0.850  0.850 |
| 臀小肌/GluteusMin | GluteusMin\_L GluteusMin\_R | 0.800  0.800 |
| 髂腰肌/Iliopsoas | Iliopsoas\_L Iliopsoas\_R | 0.850 0.850 |

Note:

* L / R: 左侧/右侧 (Left / Right)，例如 Lung\_L 为左肺，Lung\_R 为右肺。
* 肌肉名称后缀 (Max, Med, Min): 最大 / 中 / 最小 (Maximus / Medius / Minimus)，例如 GluteusMax 为臀大肌，GluteusMed 为臀中肌，GluteusMin 为臀小肌。

Note:

* L / R: Left / Right, e.g., Lung\_L is left lung, Lung\_R is right lung.
* Muscle suffix (Max, Med, Min): Maximus / Medius / Minimus, e.g., GluteusMax is gluteus maximus, GluteusMed is gluteus medius, GluteusMin is gluteus minimus.

**参考文献/reference：**

[1] U.S. Food & Drug Administration. 510(k) Premarket Notification - K230082: GE Healthcare, Auto Segmentation (CT). Silver Spring, MD: FDA; 2023. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfPMN/pmn.cfm?ID=K230082

[2] U.S. Food & Drug Administration. 510(k) Premarket Notification - K213976: MIM Software, Contour ProtégéAI (CT/MR). Silver Spring, MD: FDA; 2021. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfPMN/pmn.cfm?ID=K213976

[3] U.S. Food & Drug Administration. 510(k) Premarket Notification - K242745: Siemens Healthineers, AI-Rad Companion Organs RT (CT/MR). Silver Spring, MD: FDA; 2024. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfpmn/pmn.cfm?ID=K242745

[4] U.S. Food & Drug Administration. 510(k) Premarket Notification - K232899: Radformation, AutoContour (Model RADAC V4, CT/MR). Silver Spring, MD: FDA; 2023. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfpmn/pmn.cfm?ID=K232899

[5] U.S. Food & Drug Administration. 510(k) Premarket Notification - K242729: Radformation, AutoContour (Model RADAC V3, CT/MR). Silver Spring, MD: FDA; 2024. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfpmn/pmn.cfm?ID=K242729

[6] U.S. Food & Drug Administration. 510(k) Premarket Notification - K230685: Radformation, AutoContour (Model RADAC V2). Silver Spring, MD: FDA; 2023. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfpmn/pmn.cfm?ID=K230685

[7] U.S. Food & Drug Administration. 510(k) Premarket Notification - K220598: Radformation, AutoContour (Model RADAC V2). Silver Spring, MD: FDA; 2022. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfpmn/pmn.cfm?ID=K220598

[8] U.S. Food & Drug Administration. 510(k) Premarket Notification - K232928: Wisdom Technologies, DeepContour (V1.0, CT). Silver Spring, MD: FDA; 2023. Accessed January 6, 2026. https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfPMN/pmn.cfm?ID=K232928

[9] Akinci D'Antonoli T, Berger LK, Indrakanti AK, et al. TotalSegmentator MRI: Robust sequence-independent segmentation of multiple anatomic structures in MRI. Radiology. 2025;314(2):e241613. doi:10.1148/radiol.241613

[10] Häntze H, Xu L, Mertens CJ, et al. Segmenting whole-body MRI and CT for multiorgan anatomic structure delineation. Radiol Artif Intell. 2025;7(6):e240777. doi:10.1148/ryai.240777

[11] Chen W, Huang H, Huang J, et al. Deep learning-based medical image segmentation of the aorta using XR-MSF-U-Net. Comput Methods Programs Biomed. 2022;225:107073. doi:10.1016/j.cmpb.2022.107073

[12] Astley JR, Biancardi AM, Hughes PJ, et al. Implementable deep learning for multi-sequence proton MRI lung segmentation: A multi-center, multi-vendor, and multi-disease study. J Magn Reson Imaging. 2023;58(4):1030-1044. doi:10.1002/jmri.28643

[13] Fu Y, Mazur TR, Wu X, et al. A novel MRI segmentation method using CNN-based correction network for MRI-guided adaptive radiotherapy. Med Phys. 2018;45(11):5129-5137. doi:10.1002/mp.13221

[14] Jaitner N, Ludwig J, Meyer T, et al. Automated liver and spleen segmentation for MR elastography maps using U-Nets. Sci Rep. 2025;15(1):10762. doi:10.1038/s41598-025-95157-w

[15] Huang L, Li M, Gou S, et al. Automated segmentation method for low field 3D stomach MRI using transferred learning image enhancement network. Biomed Res Int. 2021;2021:6679603. doi:10.1155/2021/6679603

[16] Daniel AJ, Buchanan CE, Allcock T, et al. Automated renal segmentation in healthy and chronic kidney disease subjects using a convolutional neural network. Magn Reson Med. 2021;86(2):1125-1136. doi:10.1002/mrm.28768

[17] Perone CS, Calabrese E, Cohen-Adad J. Spinal cord gray matter segmentation using deep dilated convolutions. Sci Rep. 2018;8(1):5966. doi:10.1038/s41598-018-24304-3

[18] Li H, Luo H, Liu Y. Paraspinal muscle segmentation based on deep neural network. Sensors (Basel). 2019;19(12):2650. doi:10.3390/s19122650

[19] Wesselink EO, Elliott JM, Coppieters MW, et al. Convolutional neural networks for the automatic segmentation of lumbar paraspinal muscles in people with low back pain. Sci Rep. 2022;12(1):13485. doi:10.1038/s41598-022-16710-5

[20] Belzunce MA, Henckel J, Fotiadou A, et al. Automated multi-atlas segmentation of gluteus maximus from Dixon and T1-weighted magnetic resonance images. MAGMA. 2020;33(5):677-688. doi:10.1007/s10334-020-00839-3

[21] Zhuang Y, Mathai TS, Mukherjee P, et al. Segmentation of pelvic structures in T2 MRI via MR-to-CT synthesis. Comput Med Imaging Graph. 2024;112:102335. doi:10.1016/j.compmedimag.2024.102335

[22] Lei Y, Zhou J, Dong X, et al. Multi-organ segmentation in head and neck MRI using U-Faster-RCNN. Proc SPIE. 2020;11313:113133A. doi:10.1117/12.2549596

|  |  |
| --- | --- |
| 训练/调优评价标准：  Training/tuning evaluation criterion | 采用医学图像分割方法中常用的DICE评价指标[1]作为Loss函数。如果所选模型符合以下评价标准，则认为所选模型合格：   1. 训练集中Loss曲线达到收敛，相邻两次Loss迭代之差小于10-1。 2. 将模型在调优集的评价标准设置为：器官的DICE的平均值大于对应的通过标准。   The commonly used DICE evaluation metric [1] for medical image segmentation methods is used as the loss function. If the selected model meets the following evaluation criteria, it is considered qualified:   1. The loss curve in the training set converges, with a difference of less than 10-1 between the loss iterations. 2. The model's evaluation criterion in the tuning set is set as the average DICE score for the organs being greater than corresponding passing criteria.   Reference  [1] Wong K C L , Moradi M , Tang H , et al. 3D Segmentation with Exponential Logarithmic Loss for Highly Unbalanced Object Sizes[C]// International Conference on Medical Image Computing and Computer-Assisted Intervention. Springer, Cham, 2018. |

#### 设计限制/Design Limitation

对于MR器官分割，以下情况中分割结果可能不佳：

1.非标准的解剖结构(如先天性畸形、手术后改变等)或病变区域(如肿瘤、炎症等)

* 解剖变异与先天性异常：例如器官缺如/发育不全（单侧肾缺如）、器官融合（马蹄肾）、异位或骨骼系统变异，可能导致模型无法识别或错误分割。
* 术后改变与植入物：例如器官切除后，模型可能在原始位置生成假阳性分割；器官移植后位置改变、外科重建或植入物（特别是金属假体）造成的伪影，均可能导致分割错误。
* 广泛的病理改变：例如巨大的占位性病变（大肿瘤）可能导致器官体积被严重高估或轮廓无法识别；弥漫性实质病变（晚期肝硬化、重度脂肪肝）会显著降低边界准确性；大量积液/积气或肠管扩张会推移并扭曲邻近器官。

2.低对比度或噪声严重的图像

* 伪影与噪声：严重的运动伪影、磁化率伪影（或化学位移伪影）或高图像噪声会破坏纹理和形态细节，可能导致分割不连续或碎裂。
* 低分辨率或大层厚：会丢失精细的解剖细节，尤其影响小器官（如肾上腺、胆囊）的边界精确描绘。
* 快速采集序列（如单次激发序列）或高加速因子的压缩感知采集：这些技术虽然缩短了扫描时间，但会以降低信噪比、增加特定噪声或模糊为代价，影响分割精度。对于小器官或本身对比度低的结构（如胰腺与周围脂肪），可能导致分割出现空洞、边界不规则或完全漏检。

3.患者年龄小于20岁

For MR organ segmentation, the segmentation results may exhibit reduced accuracy in the following scenarios:
1. Non-standard anatomical structures (e.g., congenital anomalies, post-surgical alterations) or pathological regions (such as tumors, inflammation, etc.).

* Anatomical Variants & Congenital Anomalies: e.g., organ agenesis/hypoplasia (unilateral renal agenesis), organ fusion (horseshoe kidney), ectopic locations, or skeletal system variants, which may cause the model to fail recognition or produce erroneous segmentations.
* Post-Surgical Changes & Implants: e.g., after organ resection, the model may generate false-positive segmentations at the native location; altered organ position post-transplantation, surgical reconstruction, or implants (especially metallic prostheses causing artifacts) can all lead to segmentation errors.
* Extensive Pathological Changes: e.g., large space-occupying lesions (massive tumors) may cause severe overestimation of organ volume or complete failure to recognize its contour; diffuse parenchymal diseases (advanced cirrhosis, severe hepatic steatosis) significantly reduce boundary accuracy; massive effusion/pneumatosis or bowel distension can displace and deform adjacent organs.

2. Images with low contrast or severe noise.

* Artifacts & Noise: Severe motion artifacts, susceptibility artifacts (or chemical shift artifacts), or high image noise degrade texture and morphological details, potentially resulting in discontinuous or fragmented segmentations.
* Low Resolution or Large Slice Thickness: Loss of fine anatomical details, particularly affecting accurate boundary delineation of small organs (e.g., adrenal glands, gallbladder).
* Rapid acquisition sequences (e.g., single-shot sequences) or compressed sensing acquisitions with high acceleration factors: While shortening scan time, these techniques compromise segmentation accuracy by reducing the signal-to-noise ratio and introducing specific noise or blurring. For small organs or structures with inherently low contrast (e.g., pancreatic border), this may cause holes, irregular boundaries, or complete missed detections.

3. Patients under the age of 20.

# 风险控制措施的设计/The Design of the Risk Control Method

无风险需求，算法验证报告保证了算法的准确性和有效性。

There is no risk requirement, and the algorithm verification report ensures the accuracy and effectiveness of the algorithm.

# 网络安全的设计/The Design of the Cybersecurity

在网络安全领域，算法设计需重点关注现成框架漏洞防护和数据污染问题:

1.选择经过安全审计的开源框架或商业组件，优先采用活跃社区维护的成熟技术，降低漏洞风险‌

2.对所有输入数据实施严格校验，包括格式、长度、范围等规则，阻止恶意构造的数据注入

In the domain of cybersecurity, algorithm design should emphasize protection against vulnerabilities and prevention of data contamination within off-the-shelf frameworks:

1. Choose open-source frameworks or commercial components that have undergone rigorous security audits, prioritizing well-established technologies supported by active communities to mitigate vulnerability risks.

2. Enforce stringent validation of all input data, encompassing format, length, and range constraints, to thwart malicious data injection.

# 基本质量属性/General Quality Feature

## 可测性/Testability

对于符合输入要求的图像，算法需要保证正确性；对于临床要求的输入图像，算法需要保证稳定性和不会崩溃。

For images that satisfy the input criteria, the algorithm must guarantee accuracy. For clinically required input images, the algorithm must ensure stability and prevent system failures.

## 可扩展性考虑分析/Scalability and Extensibility

在架构中应用以下设计模式来解决可重用性问题。

• 分层体系结构

• 组件化设计

• 基于接口的计算机交互设计

To address reusability issues within your architecture, it is recommended to implement the following design patterns:

- Layered Architecture

- Component-based Design

- Interface-driven Interaction Design

## 可维护性/Maintainability

使用有良好定义和很少交互的组件，意味着组件可以在不影响整个系统稳定的情况下，被单独维护。应用以下的设计模式来解决可维护性：

• 分层体系结构

• 组件化设计

• 基于接口的计算机交互设计

The utilization of well-defined components with minimal interactions ensures that individual components can be maintained without compromising the stability of the overall system. To enhance maintainability, we recommend implementing the following design patterns:

• Layered architecture

• Component-based design

• Interface-oriented interaction design

## 可适用性/Adaptability

基于模块化的算法设计可以保证算法很方便地集成在应用，满足不同的应用需求。是依据临床应用需求来设计的，模块和模块直接所以它会满足临床需求。

The algorithm design based on modularity ensures seamless integration into applications, thereby fulfilling diverse application requirements. Designed in accordance with clinical application needs, the modular structure enables clear and direct interactions between modules, ensuring that the algorithm effectively meets clinical requirements.

# 安装和服务/Installation & Service

N.A.

# 终止实现的设计/Terminated Design

N.A.

# 未决事项/Open Issues

N.A.

**设计列表/Table of Design Keys**

|  |  |  |  |
| --- | --- | --- | --- |
| ID | Status | PRA | Rearranged |
| 1070192 | Released | No | N.A. |
| 1070189 | Released | No | N.A. |
| 1070565 | Released | No | N.A. |