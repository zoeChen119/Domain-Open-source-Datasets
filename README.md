# Domain-Open-source-Datasets

![image-20231128145243530](E:\Zoe\zoeChen119.github.io\assets\img\README\image-20231128145243530.png)



### 1.CCKS2021运营商知识图谱推理问答数据集

* **原地址**：https://tianchi.aliyun.com/dataset/109340

* **描述**：本数据集来源于CCKS2021 运营商知识图谱推理问答学术评测任务 （https://tianchi.aliyun.com/competition/entrance/531904/introduction），由阿里巴巴与中移在线服务有限公司联合提供，包含5000条训练数据、1000条测试数据，以及运营商知识图谱数据。

* **动机/需求**：

  促进NLP社区对**复杂Query（如约束句或者推理型问句）**下的KBQA技术的研究。基于知识图谱的问答系统，通过对用户输入query进行语义理解，生成结构化查询语句，从给定知识库中选择若干实体或属性值作为该问题的答案。当前知识图谱问答系统在简单句（单实体单属性）上已经取得比较好的效果，而在约束句：条件约束句、时间约束句，以及推理型问句：比较句、最值句、是否型问句以及问句中带有交集、并集和取反的问句等，其逻辑推理能力还有待提升。

  以电信运营商场景为例，比如：“不含彩铃的套餐有哪些？”、“支持长途漫游，价格低于100元的套餐有哪些？”、“神州行B套餐是5G套餐吗”等，这类需要推理的Query目前的问答系统难以回答。

  输入样例：
  q1:流量日包的开通方式？
  q2:不含彩铃的套餐有哪些？

  输出样例
  a1:“KTLLRB”
  a2:“流量月包|流量年包”

* **数据集说明**：

  本任务使用的知识库是来源于阿里巴巴和中移在线服务有限公司联合构建，包括：

  - 运营商知识图谱scheme.xlsx： 包含类型和谓词之间的上下位关系等信息；
  - triples.txt： 包含知识库主要三元组；
  - synonyms.txt： 可以用来辅助研究人员进行实体识别；
  - train.xlsx： 训练集，共5000条，包括问题/SPARQL主要语义成分/答案。
  - test1.xlsx： 初赛测试集，共1000条不含答案的测试数据。

  本次测评的问答数据来自于电信运营商业务真实数据，而不是通过模板生成，并且经过多个业务专家进行人工标注，能够保证数据的准确性和多样性。问答数据集中的问题，包含简单句、约束句和推理句，数量比例大致为4：5：1。

### 2. 华为面向通信领域的过程类事件抽取

* **原地址**：[GitHub - shenzaimin/CCKS-2021-Huawei-Event-Extraction: 华为面向通信领域的过程类事件抽取baseline方案及代码](https://github.com/shenzaimin/CCKS-2021-Huawei-Event-Extraction)

* **描述**：本次评测任务的语料来源主要是华为公司的公开故障处理案例。本次评测任务的事件类型包括：指标恶化类、软硬件异常、采集数据、核查类、配置类故障、外部事件、调整机器、操作机器等。

* **动机/需求**：

  通信领域存在多种的过程类知识，如硬件安装（基站主设备安装操作步骤）、参数配置（配置网元开通与对接相关的参数）、集成调测（网元开通调试和功能验证）、故障处理（修复网元开通或正常运行中出现的故障）等， 其中故障处理过程类知识尤为重要。通信运维过程中，通过“事件”及“事件关系”对故障过程知识进行梳理，给用户呈现故障发生的逻辑，提供故障排查和故障恢复方案，指导一线处理现网故障。

  在故障知识整理过程中，“事件抽取”与“事件共指消解”是实现故障脉络、排查步骤和恢复步骤梳理的重要手段。 

  通信领域“事件抽取”的挑战在于通信业务的复杂和任务本身的复杂，其中通信业务的在于复杂的领域长词、歧义事件、元素共用等，而任务本身的复杂在于多任务识别（包括触发词和角色识别）、元素间的依赖关系等。

  “事件共指消解”的难点在于事件元素表述多样化和事件元素缺损（漏抽取、文本描述缺损）。

* **数据集说明：**

  * 子任务一：事件抽取

  该任务目标是从自由文本中抽取事件触发词及事件角色：即给定自由文本T，抽取文本T中所有的事件集合E，对于E中的每个事件e，从文本T中抽取e的触发词（包含词、位置、分类）和各个角色（包含词、位置、分类）。

  在训练及验证数据发布阶段，我们会发布15k条左右的文本及其所标注事件元素和2k条左右的验证文本。

  训练集每行为一个json文档, “doc_id”问题文本ID， “text”为文本，“event_list”为文本的事件列表，如下：
  
  ```json
  {
  "doc_id": "0579", 
  "text": "基带板闭塞导致小区不可用", 
  "event_list": [
  			{
  			"trigger": ["SoftHardwareFault", 3, "闭塞"], 
  			"argument": [["Subject", 0, "基带板"]]
  			}, 
  			{
  			"trigger": ["SoftHardwareFault", 9, "不可用"], 
  			"argument": [["Subject", 7, "小区"]]
  			}
  		]
  }
  ```

  验证集每行为一个json：

  ```json
  {	
  "doc_id": "0579", 
  "text": "基带板闭塞导致小区不可用",
  }
  ```

  提交格式：

  ```json
  {
  "doc_id": "0579", 
  "event_list": [
        {
        "trigger": ["SoftHardwareFault", 3, "闭塞"], 
        "argument": [["Subject", 0, "基带板"]]
        }, 
        {
        "trigger": ["SoftHardwareFault", 9, "不可用"], 
        "argument": [["Subject", 7, "小区"]]
        }
  	] 
  }
  ```
  > **输入**：一段文本T
  >
  > **输出**：事件触发词和事件角色
  >
  > **示例**：
  >
  > 样例1
  >
  > ​		输入：*“将直放站小区半径参数由2000m改为10000m”*
  >
  > ​		输出：{"trigger": ["SetMachine", 14, "改为"], "argument": [["Object", 1, "直放站小区半径"], ["InitialState", 9, "2000m"], ["FinalState", 16, "10000m"]]}
  >
  > 样例2
  >
  > ​		*输入：“XX小区晚上8点之后苹果终端接入5G网络失败*”
  > ​		*输出：* *{"trigger": ["SoftHardwareFault", 14, "接入"], "argument": [["Subject", 10, "苹果终端"], ["Object", 16, "5G网络"], ["State", 20, "失败"]]}]*

  其中各事件元素及其说明如下表：

  ![img](https://pic2.zhimg.com/80/v2-f618874f2420f12264e0f970b954d72d_720w.webp)

  <center>事件元素及其说明</center>
  
  * 子任务二：事件共指消解任务

该任务的目的是给定两个自由文本及其中的事件判定两个事件是否为同一个事件。即给定文本T1、T2、T1中事件e1和T2中事件e2，判定e1和e2是否相等（其中事件类型及元素表如子任务一介绍）

> **样例1**
>
> 输入：
>
> ​		e1: {"text": "PTN链上端站交叉板隐性问题导致部分TDS站点下PS掉线率指标恶化及交互类业务异常问题", "trigger": ["IndexFault", 31, "恶化"], "argument": [["Index", 18, "TDS站点下PS掉线率指标"]]},
>
> ​		e2: {"text": "PS掉线率升高的问题", "trigger": ["IndexFault", 5, "升高"], "argument": [["Index", 0, "PS掉线率"]]} }
>
> 输出：True
>
> **样例**2：
>
> 输入：
>
> ​		e1: {"text": "特定用户协同功能开关未开启导致5GCPE无法接入19B版本的NSA组网", "trigger": ["SoftHardwareFault", 22, "接入"], "argument": [["Subject", 15, "5GCPE"], ["State", 20, "无法"], ["Object", 24, "19B版本的NSA组网"]]},
>
> ​		e2: {"text": "5G 终端无法入网。", "trigger": ["SoftHardwareFault", 7, "入网"], "argument": [["Subject", 0, "5G 终端"], ["State", 5, "无法"]]}}
>
> 输出：False

在训练及验证数据发布阶段，我们会发布15k条左右的事件对和2k条验证集。

训练集每行为一个json格式，“pair_id”为事件对ID，“eventA”和“eventB”为事件的文本及其元素(包含text，trigger，argument三个字段)，label为标签（true共指，false非共指），具体格式示例如下：

 ```json
 { 
 	"pair_id": "XXX102", 
 	"eventA": {
 				"text": "特定用户协同功能开关未开启导致5GCPE无法接入19B版本的NSA组网", 
 				"trigger": ["SoftHardwareFault", 22, "接入"], 
 				"argument": [["Subject", 15, "5GCPE"], ["State", 20, "无法"], ["Object", 24, "19B版本的NSA组网"]]
 				}, 
 	"eventB": {
 				"text": "5G终端无法入网。", 
 				"trigger": ["SoftHardwareFault", 6, "入网"], 
 				"argument": [["Subject", 0, "5终端"], ["State", 4, "无法"]]}, 
 				"label": false 
 } 
 ```

验证集格式：
 ```json
{
	"pair_id": "XXX103" , 
	"eventA": {
			"text": "特定用户协同功能开关未开启导致5GCPE无法接入19B版本的NSA组网", 
			"trigger": ["SoftHardwareFault", 22, "接入"], 
			"argument": [["Subject", 15, "5GCPE"], ["State", 20, "无法"], ["Object", 24, "19B版本的NSA组网"]]
				}, 
	"eventB": {
			"text": "5G终端无法入网。", 
			"trigger": ["SoftHardwareFault", 6, "入网"], 
			"argument": [["Subject", 0, "5终端"], ["State", 4, "无法"]]
				}
}
 ```

提交格式：

 ```json
 { 
 "pair_id": "XXX103", 
 "label": false 
 }
 ```

测试集：

在测试数据发布阶段，我们将会再发布2k条左右的文本数据集（另外会有一定数量的干扰数据不参与结果评测），其中只有的事件标注，不含共指标注结果，作为测试。格式为：
 ```json
{
"pair_id": "XXX103", 
"eventA": {
	"text": "特定用户协同功能开关未开启导致5GCPE无法接入19B版本的NSA组网", 
	"trigger": ["SoftHardwareFault", 22, "接入"], 
	"argument": [["Subject", 15, "5GCPE"], ["State", 20, "无法"], ["Object", 24, "19B版本的NSA组网"]]}, 
	"eventB": {"text": "5G终端无法入网。", 
	"trigger": ["SoftHardwareFault", 6, "入网"], 
	"argument": [["Subject", 0, "5终端"], ["State", 4, "无法"]]
	} 
}
 ```

提交结果格式：
 ```json
{
"pair_id": "XXX103", 
"label": false
}
 ```

https://zhuanlan.zhihu.com/p/466223448

### 3. GAIA：智能运维领域通用公开数据集

https://zhuanlan.zhihu.com/p/404102376

### 4. MobileCS (移动客户服务) dialog数据集

https://opendatalab.org.cn/OpenDataLab/MobileCS

中国移动的真实用户和客户服务人员之间的真实对话记录，隐私信息匿名。

适用任务：实体抽取/三元组构建/意图识别

![image-20231128145126809](E:\Zoe\zoeChen119.github.io\assets\img\README\image-20231128145126809.png)

### 5. Kaggle项目：电信客户流失分析

https://zhuanlan.zhihu.com/p/364435834

### 6. 客服多轮对话数据集

在美团等食品服务电子商务平台中，基于用户评论，文本对话和电话对话，提出了一个新的大型中文事件检测数据集。

适用任务：实体抽取/时间抽取/标签分类

https://github.com/myeclipse/MUSIED/blob/main/data/README.md

![image-20231128145210405](E:\Zoe\zoeChen119.github.io\assets\img\README\image-20231128145210405.png)