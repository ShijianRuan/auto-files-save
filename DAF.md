|  |  |
| --- | --- |
|  |  |
| **项目名称/Project Name** |  |
| **产品代号/Product Code** |  |

|  |
| --- |
| **Subtitle**  **数据收集规范/Data Gathering Specification**  XXXXXXX-DAF-XXX-XX  生效日期/Valid from: See Windchill |

© 联影医疗 版权所有

© United Imaging Healthcare Reserved

**更改记录/History**

|  |  |  |  |
| --- | --- | --- | --- |
| **版本/Version** | **作者/Author** | **变更号/CR No.** | **主要变更内容/Change Contents** |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

**目录/Table of Contents**

[更改记录/History 2](#_Toc213059625)

[目录/Table of Contents 3](#_Toc213059626)

[1 介绍/Introduction 4](#_Toc213059627)

[1.1 范围/Scope 4](#_Toc213059628)

[1.2 定义和缩略语/Definitions and Abbreviations 4](#_Toc213059629)

[1.2.1 定义/Definitions 4](#_Toc213059630)

[1.2.2 缩略语/Abbreviations 4](#_Toc213059631)

[1.3 参考文件/References 4](#_Toc213059632)

[2 多模态肿瘤追踪应用/MM Oncology 5](#_Toc213059633)

[2.1 CT器官分割算法/ CT Organ Segmentation Algorithm 5](#_Toc213059634)

[2.1.1 数据采集/Data Acquisition 5](#_Toc213059635)

[2.1.2 数据整理/Data Processing 5](#_Toc213059636)

[2.1.3 数据标注/Data Annotation 6](#_Toc213059637)

[2.1.4 数据集构建/Construction of Data Sets 10](#_Toc213059638)

[2.1.5 数据集质量属性要求/Data Set Quality Attribute Requirements 13](#_Toc213059639)

[2.1.6 数据和数据集变更/Change of Data and Data Sets 15](#_Toc213059640)

[2.1.7 未决事项/Open Issues 15](#_Toc213059641)

[2.2 MR器官分割算法/ MR Organ Segmentation Algorithm 15](#_Toc213059642)

[2.2.1 数据采集/Data Acquisition 15](#_Toc213059643)

[2.2.2 数据整理/Data Processing 16](#_Toc213059644)

[2.2.3 数据标注/Data Annotation 16](#_Toc213059645)

[2.2.4 数据集构建/Construction of Data Sets 20](#_Toc213059646)

[2.2.5 数据集质量属性要求/Data Set Quality Attribute Requirements 22](#_Toc213059647)

[2.2.6 数据和数据集变更/Change of Data and Data Sets 24](#_Toc213059648)

[2.2.7 未决事项/Open Issues 24](#_Toc213059649)

# 介绍/Introduction

本文档描述uOmnispace.MI 中深度学习相关算法的数据收集规范。

This document describes the data gathering specification of deep learning related algorithms in

uOmnispace.MI workstation.

## 范围/Scope

本文档适用于以下应用：多模态肿瘤追踪应用。

This document is applicable to MM Oncology application.

## 定义和缩略语/Definitions and Abbreviations

### 定义/Definitions

N.A.

### 缩略语/Abbreviations

|  |  |  |
| --- | --- | --- |
| CT | Computed Tomography | 计算机断层扫描 |
| MR | Magnetic Resonance | 核磁共振 |

## 参考文件/References

[1]中华医学会放射学分会. 放射科管理规范与质控标准(2017版). 北京：人民卫生出版社，2017./Management Principles and Quality Control Standards for Department of Radiology (2017 Edition)

[2]基于TotalSegmentator 的CT 图像鲁棒分割[J]。放射学：人工智能， 2023,5(5):e230024。

TotalSegmentator: robust segmentation of 104 anatomic structures in CT images[J]. Radiology: Artificial Intelligence, 2023, 5(5): e230024.数据采集/Data Acquisition

# 多模态肿瘤追踪应用/MM Oncology

## CT器官分割算法/ CT Organ Segmentation Algorithm

### 数据采集/Data Acquisition

#### 采集设备的要求/Requirements for acquisition equipment

要求采集设备可支持扫描及输出符合DICOM标准的CT数据；不同采集设备输出的数据，其差异性不是CT器官分割算法研发的敏感因素，故对采集设备的制造商不做特定要求。

Require the collection device to support scanning and outputting CT data that meets DICOM standards; The difference in data output from different collection devices is not a sensitive factor in the development of CT organ segmentation algorithm, so there are no specific requirements for the manufacturer of the collection devices.

#### 采集过程质控的要求/ Acquisition process quality control requirements

采集人员应具备CT 成像系统扫描操作技能，熟悉CT 的采集规范和流程。

The acquisition personnel should have the scanning operation skills of CT imaging system and be familiar

with the acquisition specification and process of CT.

#### 采集数据的要求/Requirements for acquisition data

1. 采集数据为CT 图像

2. 图像质量较好，各种伪影及噪声不明显

3. 采集的数据应覆盖头部、颈部、胸部、腹部、盆腔等部位

1. The acquisition data is CT image

2. The image quality is good. All kinds of artifacts and noise are not obvious

3. The collected data should cover the head, neck, thorax, abdomen, pelvis.

### 数据整理/Data Processing

#### 基础数据的要求/Requirements for foundation data

模型的训练是基于TotalSegmentator CT数据集 (https://doi.org/10.5281/zenodo.6802613)。该公共可用的数据包括1228 例患者的CT 扫描图像，数据来源于瑞士巴塞尔大学医院公开的来自不同扫描设备和成像协议CT 扫描影像，涵盖多种疾病类型及正常病例。所有图像均重采样至1.5 mm 各向同性分辨率。每个病例提供所包含器官的金标准标注，由资深放射科医师进行标注及质量验证。来自合作医院的历史扫描数据被收集并标注后用作模型的验证。训练集与测试集均应覆盖头部、颈部、胸部、腹部和盆腔。

The training of the model was carried out based on the TotalSegmentator CT dataset (https://doi.org/10.5281/zenodo.6802613). The publicly available data includes CT scan images of 1228 patients. The data is sourced from the CT scan images of different scanning devices and imaging protocols publicly released by the University Hospital Basel in Switzerland, covering various disease types and normal cases. All images were resampled to 1.5-mm isotropic resolution. For each case, the ground truth including the organs is provided, which is annotated and undergoes quality verification by senior radiologists. Historical scan data collected from collaborating hospitals were annotated and used for model validation. The training and testing sets should both cover the head, neck, thorax, abdomen, pelvis.

##### 数据预处理/清洗要求/Data preprocessing & cleaning requirements

获取到的数据为已完成检查的数据，符合临床检查要求，不进行数据清洗。

The data obtained is the data of the completed examination, which meets the requirements of clinical examination, and no data cleaning is carried out.

##### 基础数据分布及依据/Distribution and basis of foundation data

|  |  |  |  |
| --- | --- | --- | --- |
| 样本类型/data type | 样本量/data size（sets） | 样本分布/data distribution | 备注/note |
| CT图像/CT data | 1200-1320 | 覆盖不同年龄，不同性别，不同部位，不同管电流和不同管电压的数据。  Covering data of different ages, genders, body parts, tube currents and tube voltages. | N.A. |

### 数据标注/Data Annotation

#### 标注任务描述/Annotation task description

|  |  |
| --- | --- |
| 数据模态/ Data modality | 图像/image |
| 执行主体/Execution subject | 人工标注,半自动标注/manual annotation, semiautomatic  annotation |
| 标注结果格式/Format of annotation results | 非结构化标注/unstructured annotation |
| 标注结果性质/Nature of annotation results | GT值、参考标准、金标准/GT , reference standard,  gold standard |
| 标注结果形式/Annotation result format | 分割/segmentation |

#### 标注资源管理/Resource management of data annotation

##### 人员管理/Personnel management

|  |  |
| --- | --- |
| 角色/Role | 资质要求/ Qualification Requirements |
| 标注人员/  Tagging staff | 系统学习了数据标记标注方法、操作流程、规范要求等相关知识和技能；经培训了解人体各个器官的解剖位置和结构  Systematically learned data labeling methods, operational procedures, and standards and requirements, and other related knowledge and skills. After training, gained an understanding of the anatomical structure and positioning of human organs. |
| 质量评估人员/Quality evaluator | 接受过CT 人体器官解剖结构培训，且有2 年及以上的标注经验；或有临床背景，且从事影像相关工作二年及以上  Trained in CT human organ anatomy with 2 or more years of labeling experience, or clinical background and two or more years of imaging related experience. |
| 仲裁人员/  Arbitrator | 有临床背景，且从事影像相关经验三年及以上。  Clinical background and three or more years of imaging related experience. |

##### 基础设施管理/Infrastructure management

|  |  |
| --- | --- |
|  | 要求/Requirements |
| 标注场所/  Environment | 操作系统：WIN操作系统  模拟环境标注  Operating system: WIN operating system  Analog environment labeling |

##### 标注工具管理/Tool management of data annotation

|  |  |
| --- | --- |
| 标注软件/  Label software | ITK-SNAP 3.4（Open Source） |

#### 标注过程质控/Annotation process quality control

##### 标注人员职责/Annotation personnel responsibilities

|  |  |  |
| --- | --- | --- |
| 角色/Role | 职责/ Duties and responsibilities | 数量/Number |
| 标注人员/Tagging staff | 数据标注  Data annotation | 2 |
| 仲裁人员/Arbitrator | 针对标注分歧情况进行仲裁决定  Arbitration decisions shall be made in case of differences in labeling | 1 |
| 质量评估人员/Quality evaluator | 对于标记质量进行评估确认  Quality evaluator for marking quality | 1 |

##### 标注流程/Annotation process

训练集标注流程：两名分别拥有 3 年（M.S.）和 6 年（H.C.B.）体部成像经验的医生对标注工作进行监督[2]。使用诺拉成像平台（NoraView）进行手动分割或优化生成的分割结果。标注流程如下：

利用现有模型进行初始分割：如果针对某一结构存在公开可用的模型，则使用该模型创建初始分割结果，随后对其进行手动验证和优化。

迭代学习：在完成对前 5 名患者的手动分割后，训练一个初步的 nnU-Net 模型。如有需要，对该模型的预测结果进行手动优化。在对 5 名、20 名和 100 名患者的分割结果依次进行审查和优化后，重新训练 nnU-Net模型。

最终审查与修正：对所有 CT 检查的标注进行人工审查，必要时进行修正。

无需进行多轮标注。

Annotation process of the training set: Two physicians with 3 (M.S.) and 6 (H.C.B.) years of body imaging experience supervised the annotation work [2]. The Nora Imaging Platform was used for manual segmentation or refining generated segmentations.

The annotation process was as follows:

Initial Segmentation with Existing Models: If a public model for a structure was available, it was used to create an initial segmentation, which was then manually validated and refined.

Iterative Learning Approach: After manually segmenting the first five patients, a preliminary nnU-Net was trained. Its predictions were manually refined if needed. The nnU-Net was retrained after reviewing and refining the segmentations of 5, 20, and 100 patients successively.

Final Review and Correction: All CT examinations had annotations that were manually reviewed, and corrections were made whenever necessary.

Multiple rounds of annotation are not required.

测试集标注流程：在ITK-SNAP 3.4中打开CT数据，标记人员先对 CT 图像进行视觉评估，识别出图像中所包含的需要标注的器官，然后在图像上手动标注所有目标器官区域，使得掩膜与器官边界贴合（如下图所示）。在完成第一轮标记之后，他们会相互检查彼此的标注。最后，质量评估人员会对标记进行检查和修改，以此确保金标准的正确性。

Annotation process of the testing set: In ITK-SNAP 3.4, annotators first conduct a visual assessment of the CT images to identify the organs requiring annotation. They then manually annotate all target organ regions in the images, ensuring the masks closely adhere to the organ boundaries (as shown in the figure below). After the first round of annotations, they cross-check each other’s labels. Finally, quality evaluators review and refine the annotations to ensure the accuracy of the gold standard.

![](images/9e20b769e961.png)

##### 标注规则/ Annotation rules

本次临床标注是通过参考《放射科管理规范与质控标准》（2017版）而制定。

The clinical diagnosis and treatment criteria is made according to “Management Principles and Quality Control Standards for Department of Radiology, 2017”.

##### 分歧处理/Disagreement handling

本次标注按照以上临床规范进行。如若标注人员和质量评估人员产生分歧，双方协商解决。如无法协商解决，可将分歧提交给仲裁人员进行评定。

Data gathering procedure follows above clinical diagnosis and treatment criteria. Any disputes arising from the procedure should be settled through mutual negotiation between labeling staff and quality evaluator. In case no settlement can be reached between the two parties, the case under dispute shall be submitted for the arbitrator.

##### 可追溯性/Traceability

数据通过文件服务器管理维护，提供给算法、标注及测试人员。

The data is managed and maintained by file server and provided to algorithm, annotation and testing personnel.

#### 标注质量评估/Annotation quality assessment

|  |  |
| --- | --- |
| 质量评估人员  Quality evaluator | 接受过 CT 人体器官解剖结构培训，且有 2 年及以上的标注经验；或有临床背景，且从事影像相关工作二年及以上  Trained in CT human organ anatomy with 2 or more years of labeling experience, or clinical background and two or more years of imaging-related experience. |
| 评估方法  Assessment method | 质量评估人员观察标记结果，通过影像经验进行主观评估。  Quality assessors observe the marking results and conduct subjective assessments through clinical experience. |
| 评估指标  Assessment criterion | 器官的解剖结构是否标注合理，边界是否准确。  Is the anatomical structure of the organs properly labeled and the boundaries accurate. |
| 通过准则  Pass criterion | 标记的器官掩模与器官形状贴合。  The annotation of organ mask matches the shape of organ. |

#### 标注数据分布及依据/Annotation data distribution and basis

参考基础数据分布及依据。

Refer to Distribution and basis of foundation data.

### 数据集构建/Construction of Data Sets

#### 数据集构建原则/Principles of data sets construction

使用公开数据集TotalSegmentator CT经过预处理后作为训练输入；使用新搜集的数据作为测试集；确保数据集间无交集。

The publicly available dataset TotalSegmentator CT, after being preprocessed, was treated as the training input; newly collected data was used as the testing set; Make sure there is no intersection between the datasets.

#### 训练集/Training sets

|  |  |  |  |
| --- | --- | --- | --- |
| 来源/ Data source | 样本类型/ Data type | 样本量区间/ Sample size interval | 样本分布/ Data distribution |
| 公开数据集/  Public Dataset | CT 数据/ CT Data | 1150-1250 | 覆盖不同年龄，不同性别，不同部位，不同管电流和不同管电压的数据。  Covering data of different ages, genders, body parts, tube currents and tube voltages. |

|  |  |  |  |  |
| --- | --- | --- | --- | --- |
| 扩增范围/  Augmentation scope | 扩增方式/  Augmentation mode | 扩增方法/  Augmentation method | 扩增倍数/  Augmentation factor | 是否对软件的产生影响及风险/  Impact and risks on software production |
| 所有数据/  All data | 在线/  Online | x、y、z三个轴随机翻转；  x、y、z三个轴随机旋转；  随机弹性形变；  随机尺度缩放；  随机伽马校正；  随机亮度调整；  随机对比度变化；  随机添加高斯噪声；  随机模拟低分辨率。  Random flipping along the x, y, and z axes;  Random rotation along the x, y, and z axes;  Random elastic deformation;  Random scale scaling;  Random gamma correction;  Random brightness adjustment;  Random contrast change;  Random addition of Gaussian noise;  Random simulation of low resolution. | 1:10 | N.A. |

#### 调优集/Tuning sets

无需调优集。

No tuning set is required.

#### 测试集/Testing sets

|  |  |  |  |
| --- | --- | --- | --- |
| 来源/ Data source | 样本类型/ Data type | 样本量区间/ Sample size interval | 样本分布/ Data distribution |
| 医院或历史数据/  Hospital or historical  data | CT 数据/ CT Data | 50-70 | 覆盖不同年龄，不同性别，不同部位，不同管电流和不同管电压的数据。  Covering data of different ages, genders, body parts, tube currents and tube voltages. |

### 数据集质量属性要求/Data Set Quality Attribute Requirements

|  |  |  |
| --- | --- | --- |
| **质量属性** | **定义/描述** | **具体要求** |
| 准确性 | 对数据内容正确、形式有效的一种度量。  [来源:GB/T11457-2006,2.22,有修改] | 医学图像标准结果应符合临床金标准。 |
| 完备性 | 数据集包含的信息能覆盖数据集预期用途的程度。 | 医学影像数据的DICOM现场信息包括设备型号、病人信息等。 |
| 唯一性 | 同一数据集或子集内的数据元应是唯一的。同一数据集的各个子集应是可区分的。 | 数据集中的图像是唯一的，不同图像序列之间不存在重复的图像。 |
| 一致性 | 在文档、系统或系统部件的各部分之间，一致、标准化、无矛盾的程度。在数据集的各阶段、部分之间,一致、标准化、无矛盾的程度。  [来源:GB/T11457-2006,2.320,有修改] | 内部一致性：同一受试者的图像数据在采集、预处理、标注、构建以及存储等过程中，关键特征保持一致；  外部一致性：来自不同医院的采样数据在关键数据特征方面保持一致。 |
| 确实性 | 数据集真实和可信的程度。 | 数据应来自真实的临床数据采集流程；数据采集涉及的设备、人员、方法符合技术标准、临床规范或专家共识。 |
| 时效性 | 数据集管理的各个阶段所需时限符合预期的程度。 | 清洗和预处理应在数据采集后的7天内完成。 |
| 可访问性 | 数据集可被访问的程度。 | 经过授权的用户可以预览和复制数据集。 |
| 依从性 | 数据集依从的标准规范、专家共识、操作规程或其他参考文献。 | 医学图像数据格式应符合DICOM3.0格式、mhd格式、nii格式或其他常用格式。 |
| 保密性 | 数据对未授权的个人、实体或过程不可用或不泄露的特性。  [来源:GB/T29246-2017,2.12,有修改] | 采取措施确保其只能被授权用户访问。隔离使用的数据集应具有数据集授权访问机制、隔离保护机制，应具有防止数据泄露、数据篡改、数据丢失的措施，如数据匿名化、物理隔离、数据审计等。 |
| 资源利用性 | 执行数据集相关任务需要的资源消耗。如访问、读取数据、预览、检索等任务需要的软件、硬件、网络配置。 | 存储图像序列需要的硬盘空间不小于100GB。 |
| 精度 | 对于说明的量的精确或差异的程度。  [来源:GB/T11457-2006,2.1160] | 医学图像的标注结果与目标结构的形状贴合。 |
| 可追溯性 | 人工智能医疗器械的设计开发过程、生产过程、使用过程和更新过程能被记录的程度。 | a) 原始数据来源具有合规性证明;  b) 原始数据核查记录、数据整理记录、数据标注记录；  c) 标注工具或平台使用记录；  d) 数据维护与备份记录；  e) 数据更新记录； |
| 可理解性 | 数据集中采用用户可理解的术语，对数据元、元数据和标注结果的含义提供解释。 | 医学图像数据的标注结果可以直接显示在图像上。每一个医学图像数据的分类有明确的定义。 |
| 可得性 | 数据集在投入使用时可操作或可利用的程度。  [来源:GB/T11457-2006,2.115, 有修改] | 数据集可以被读取、分析、索引等。 |
| 可移植性 | 数据集能被安装、替换或从一个系统移动到另一个系统中,并保持已有质量的属性。 | 数据集可以在不同的操作系统上使用。 |
| 可恢复性 | 数据库在使用过程中保持质量并抵御失效事件的程度。 | 数据集的使用和管理过程采用了备份和故障恢复机制，可以从系统故障中恢复。 |
| 代表性 | 数据集样本的组成、比例、人群分布特征、数据的多样性接近应用场景的程度。 | 医学图像数据集的分布应符合2.1.2.1 的要求。 |

#

### 数据和数据集变更/Change of Data and Data Sets

在算法训练、调优或测试验证时，如发现数据或数据集无法满足要求，确需变更数据或数据集的，应遵循以下变更规则：

1. 数据变更后，数据集报告中应记录变更内容；
2. 数据集若有数据新增，数据集报告中应记录新增数据的描述；
3. 数据集若有数据退役，数据集报告中应保留退役数据的记录，且退役数据需单独存储。

During algorithm training, tuning or test verification, if it is found that the data or dataset cannot meet the requirements and it is necessary to change the data or dataset, the following change rules should be followed:

1. After data changes, the changes should be recorded in the dataset report.

2. If there is new data in the dataset, the description of the new data should be recorded in the dataset report.

3. If there is data decommissioning in the dataset, the records of decommissioning data should be kept in the

dataset report, and the decommissioning data should be stored separately.

### 未决事项/Open Issues

N.A.

## MR器官分割算法/ MR Organ Segmentation Algorithm

### 数据采集/Data Acquisition

#### 采集设备的要求/Requirements for acquisition equipment

要求采集设备可支持扫描及输出符合DICOM标准的MR数据；不同采集设备输出的数据，其差异性不是MR器官分割算法研发的敏感因素，故对采集设备的制造商不做特定要求。

Require the collection device to support scanning and outputting MR data that meets DICOM standards; The difference in data output from different collection devices is not a sensitive factor in the development of MR organ segmentation algorithm, so there are no specific requirements for the manufacturer of the collection devices.

#### 采集过程质控的要求/ Acquisition process quality control requirements

采集人员应具备MR成像系统扫描操作技能，熟悉MR的采集规范和流程。

The acquisition personnel should have the scanning operation skills of MR imaging system and be familiar

with the acquisition specification and process of MR.

#### 采集数据的要求/Requirements for acquisition data

1. 采集数据为MR图像

2. 图像质量较好，各种伪影及噪声不明显

3. 采集的数据应覆盖头部、颈部、胸部、腹部、盆腔等部位

1. The acquisition data is MR image

2. The image quality is good. All kinds of artifacts and noise are not obvious

3. The collected data should cover the head, neck, thorax, abdomen, pelvis.

### 数据整理/Data Processing

#### 基础数据的要求/Requirements for foundation data

##### 数据预处理/清洗要求/Data preprocessing & cleaning requirements

获取到的数据为已完成检查的数据，符合临床检查要求，不进行数据清洗。

The data obtained is the data of the completed examination, which meets the requirements of clinical examination, and no data cleaning is carried out.

##### 基础数据分布及依据/Distribution and basis of foundation data

|  |  |  |  |
| --- | --- | --- | --- |
| 样本类型/data type | 样本量/data size（sets） | 样本分布/data distribution | 备注/note |
| MR图像/MR data | 520-600 | 覆盖不同年龄，不同性别，不同解剖序列类型，不同部位的数据。  Covering data of different ages, genders, anatomical sequence types, and body parts. | N.A. |

### 数据标注/Data Annotation

#### 标注任务描述/Annotation task description

|  |  |
| --- | --- |
| 数据模态/ Data modality | 图像/image |
| 执行主体/Execution subject | 人工标注,半自动标注/manual annotation, semiautomatic  annotation |
| 标注结果格式/Format of annotation results | 非结构化标注/unstructured annotation |
| 标注结果性质/Nature of annotation results | GT值、参考标准、金标准/GT , reference standard,  gold standard |
| 标注结果形式/Annotation result format | 分割/segmentation |

#### 标注资源管理/Resource management of data annotation

##### 人员管理/Personnel management

|  |  |
| --- | --- |
| 角色/Role | 资质要求/ Qualification Requirements |
| 标注人员/  Tagging staff | 系统学习了数据标记标注方法、操作流程、规范要求等相关知识和技能  经培训了解人体各个器官的解剖位置和结构  Systematically learned data labeling methods, operational procedures, and standards and requirements, and other related knowledge and skills. After training, gained an understanding of the anatomical structure and positioning of human organs. |
| 质量评估人员/Quality evaluator | 接受过MR人体器官解剖结构培训，且有2 年及以上的标注经验；或有临床背景，且从事影像相关工作二年及以上  Trained in MR human organ anatomy with 2 or more years of labeling experience, or clinical background and two or more years of imaging related experience. |
| 仲裁人员/  Arbitrator | 有临床背景，且从事影像相关经验三年及以上。  Clinical background and three or more years of imaging related experience. |

##### 基础设施管理/Infrastructure management

|  |  |
| --- | --- |
|  | 要求/Requirements |
| 标注场所/  Environment | 操作系统：WIN操作系统  模拟环境标注  Operating system: WIN operating system  Analog environment labeling |

##### 标注工具管理/Tool management of data annotation

|  |  |
| --- | --- |
| 标注软件/  Label software | ITK-SNAP 3.4（Open Source） |

#### 标注过程质控/Annotation process quality control

##### 标注人员职责/Annotation personnel responsibilities

|  |  |  |
| --- | --- | --- |
| 角色/Role | 职责/ Duties and responsibilities | 数量/Number |
| 标注人员/  Tagging staff | 数据标注  Data annotation | 2 |
| 仲裁人员/  Arbitrator | 针对标注分歧情况进行仲裁决定  Arbitration decisions shall be made in case of differences in labeling | 1 |
| 质量评估人员/Quality evaluator | 对于标记质量进行评估确认  Quality evaluator for marking quality | 1 |

##### 标注流程/Annotation process

在ITK-SNAP 3.4中打开MR数据，标记人员先对 MR 图像进行视觉评估，识别出图像中所包含的需要分割的器官，然后在图像上手动标注所有目标器官区域，使得掩膜与器官边界贴合（如下图所示）。在完成第一轮标记之后，他们会相互检查彼此的标注。最后，质量评估人员会对标记进行检查和修改，以此确保金标准的正确性。

In ITK-SNAP 3.4, annotators first conduct a visual assessment of the MR images to identify the organs requiring annotation. They then manually annotate all target organ regions in the images, ensuring the masks closely adhere to the organ boundaries (as shown in the figure below). After the first round of annotations, they cross-check each other’s labels. Finally, quality evaluators review and refine the annotations to ensure the accuracy of the gold standard.

![](images/ae2df6ec3514.png)

##### 标注规则/ Annotation rules

本次临床标注是通过参考《放射科管理规范与质控标准》（2017版）而制定。

The clinical diagnosis and treatment criteria is made according to “Management Principles and Quality Control Standards for Department of Radiology, 2017”.

##### 分歧处理/Disagreement handling

本次标注按照以上临床规范进行。如若标注人员和质量评估人员产生分歧，双方协商解决。如无法协商解决，可将分歧提交给仲裁人员进行评定。

Data gathering procedure follows above clinical diagnosis and treatment criteria. Any disputes arising from the procedure should be settled through mutual negotiation between labeling staff and quality evaluator. In case no settlement can be reached between the two parties, the case under dispute shall be submitted for the arbitrator.

##### 可追溯性/Traceability

数据通过文件服务器管理维护，提供给算法、标注及测试人员。

The data is managed and maintained by file server and provided to algorithm, annotation and testing personnel.

#### 标注质量评估/Annotation quality assessment

|  |  |
| --- | --- |
| 质量评估人员  Quality evaluator | 接受过 MR 人体器官解剖结构培训，且有 2 年及以上的标注经验；或有临床背景，且从事影像相关工作二年及以上  Trained in MR human organ anatomy with 2 or more years of labeling experience, or clinical background and two or more years of imaging related experience. |
| 评估方法  Assessment method | 质量评估人员观察标记结果，通过影像经验进行主观评估。  Quality assessors observe the marking results and conduct subjective assessments through clinical experience. |
| 评估指标  Assessment criterion | 器官的解剖结构是否标注合理，边界是否准确。  Is the anatomical structure of the organs properly labeled and the boundaries accurate. |
| 通过准则  Pass criterion | 标记的器官掩模与器官形状贴合。  The annotation of organ mask matches the shape of organ. |

#### 标注数据分布及依据/Annotation data distribution and basis

参考基础数据分布及依据。

Refer to Distribution and basis of foundation data.

### 数据集构建/Construction of Data Sets

#### 数据集构建原则/Principles of data sets construction

根据标注的MR器官图像数据集，从中随机抽取获得训练集和测试集，并确保数据集之间无交集。

Based on the annotated MR organ image dataset, randomly sample to obtain the training set and testing set, ensuring that there is no intersection between the datasets.

#### 训练集/Training sets

|  |  |  |  |
| --- | --- | --- | --- |
| 来源/ Data source | 样本类型/ Data type | 样本量区间/ Sample size interval | 样本分布/ Data distribution |
| 医院或历史  数据/  Hospital or historical data | MR数据/ MR Data | 470-530 | 覆盖不同年龄，不同性别，不同解剖序列类型和不同部位的数据。  Covering data of different ages, genders, anatomical sequence types, and body parts. |

|  |  |  |  |  |
| --- | --- | --- | --- | --- |
| 扩增范围/  Augmentation  scope | 扩增方式/  Augmentation mode | 扩增方法/  Augmentation method | 扩增倍数/  Augmentation factor | 是否对软件的产生影响及风险/  Impact and risks on software production |
| 所有数据/  All data | 在线/  Online | x、y、z三个轴随机翻转；  x、y、z三个轴随机旋转；  随机弹性形变；  随机尺度缩放；  随机伽马校正；  随机亮度调整；  随机对比度变化；  随机添加高斯噪声；  随机模拟低分辨率。  Random flipping along the x, y, and z axes;  Random rotation along the x, y, and z axes;  Random elastic deformation;  Random scale scaling;  Random gamma correction;  Random brightness adjustment;  Random contrast change;  Random addition of Gaussian noise;  Random simulation of low resolution. | 1:10 | N.A. |

#### 调优集/Tuning sets

无需调优集。

No tuning set is required.

#### 测试集/Testing sets

|  |  |  |  |
| --- | --- | --- | --- |
| 来源/ Data source | 样本类型/ Data type | 样本量区间/ Sample size interval | 样本分布/ Data distribution |
| 医院或历史数据/  Hospital or historical  data | MR 数据/ MR Data | 50-70 | 覆盖不同年龄，不同性别，不同解剖序列类型和不同部位的数据。  Covering data of different ages, genders, anatomical sequence types, and body parts. |

### 数据集质量属性要求/Data Set Quality Attribute Requirements

|  |  |  |
| --- | --- | --- |
| **质量属性** | **定义/描述** | **具体要求** |
| 准确性 | 对数据内容正确、形式有效的一种度量。  [来源:GB/T11457-2006,2.22,有修改] | 医学图像标准结果应符合临床金标准。 |
| 完备性 | 数据集包含的信息能覆盖数据集预期用途的程度。 | 医学影像数据的DICOM现场信息包括设备型号、病人信息等。 |
| 唯一性 | 同一数据集或子集内的数据元应是唯一的。同一数据集的各个子集应是可区分的。 | 数据集中的图像是唯一的，不同图像序列之间不存在重复的图像。 |
| 一致性 | 在文档、系统或系统部件的各部分之间，一致、标准化、无矛盾的程度。在数据集的各阶段、部分之间,一致、标准化、无矛盾的程度。  [来源:GB/T11457-2006,2.320,有修改] | 内部一致性：同一受试者的图像数据在采集、预处理、标注、构建以及存储等过程中，关键特征保持一致；  外部一致性：来自不同医院的采样数据在关键数据特征方面保持一致。 |
| 确实性 | 数据集真实和可信的程度。 | 数据应来自真实的临床数据采集流程；数据采集涉及的设备、人员、方法符合技术标准、临床规范或专家共识。 |
| 时效性 | 数据集管理的各个阶段所需时限符合预期的程度。 | 清洗和预处理应在数据采集后的7天内完成。 |
| 可访问性 | 数据集可被访问的程度。 | 经过授权的用户可以预览和复制数据集。 |
| 依从性 | 数据集依从的标准规范、专家共识、操作规程或其他参考文献。 | 医学图像数据格式应符合DICOM3.0格式、mhd格式、nii格式或其他常用格式。 |
| 保密性 | 数据对未授权的个人、实体或过程不可用或不泄露的特性。  [来源:GB/T29246-2017,2.12,有修改] | 采取措施确保其只能被授权用户访问。隔离使用的数据集应具有数据集授权访问机制、隔离保护机制，应具有防止数据泄露、数据篡改、数据丢失的措施，如数据匿名化、物理隔离、数据审计等。 |
| 资源利用性 | 执行数据集相关任务需要的资源消耗。如访问、读取数据、预览、检索等任务需要的软件、硬件、网络配置。 | 存储图像序列需要的硬盘空间不小于100GB。 |
| 精度 | 对于说明的量的精确或差异的程度。  [来源:GB/T11457-2006,2.1160] | 医学图像的标注结果与目标结构的形状贴合。 |
| 可追溯性 | 人工智能医疗器械的设计开发过程、生产过程、使用过程和更新过程能被记录的程度。 | a) 原始数据来源具有合规性证明;  b) 原始数据核查记录、数据整理记录、数据标注记录；  c) 标注工具或平台使用记录；  d) 数据维护与备份记录；  e) 数据更新记录； |
| 可理解性 | 数据集中采用用户可理解的术语，对数据元、元数据和标注结果的含义提供解释。 | 医学图像数据的标注结果可以直接显示在图像上。每一个医学图像数据的分类有明确的定义。 |
| 可得性 | 数据集在投入使用时可操作或可利用的程度。  [来源:GB/T11457-2006,2.115, 有修改] | 数据集可以被读取、分析、索引等。 |
| 可移植性 | 数据集能被安装、替换或从一个系统移动到另一个系统中,并保持已有质量的属性。 | 数据集可以在不同的操作系统上使用。 |
| 可恢复性 | 数据库在使用过程中保持质量并抵御失效事件的程度。 | 数据集的使用和管理过程采用了备份和故障恢复机制，可以从系统故障中恢复。 |
| 代表性 | 数据集样本的组成、比例、人群分布特征、数据的多样性接近应用场景的程度。 | 医学图像数据集的分布应符合2.2.2.1 的要求。 |

### 数据和数据集变更/Change of Data and Data Sets

在算法训练、调优或测试验证时，如发现数据或数据集无法满足要求，确需变更数据或数据集的，应遵循以下变更规则：

1. 数据变更后，数据集报告中应记录变更内容；
2. 数据集若有数据新增，数据集报告中应记录新增数据的描述；
3. 数据集若有数据退役，数据集报告中应保留退役数据的记录，且退役数据需单独存储。

During algorithm training, tuning or test verification, if it is found that the data or dataset cannot meet the requirements and it is necessary to change the data or dataset, the following change rules should be followed:

1. After data changes, the changes should be recorded in the dataset report.

2. If there is new data in the dataset, the description of the new data should be recorded in the dataset report.

3. If there is data decommissioning in the dataset, the records of decommissioning data should be kept in the

dataset report, and the decommissioning data should be stored separately.

### 未决事项/Open Issues

N.A.