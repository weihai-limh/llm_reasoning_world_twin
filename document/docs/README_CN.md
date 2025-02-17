# llm_reasoning_world_twin
<br>LLM推理数字孪生模型
<br>
<br>数字孪生对象是包含了语义描述文件及几何文件的聚合体.
<br>项目通过大语言模型对现实世界的数字孪生对象进行推理.
<br>由于推理结果包含了数字孪生对象所以可以通过图形引擎模拟推理结果
<br>并通过IOT投射到现实世界中使推理结果在现实中被执行.
![llm_reasoning_flowchart](https://github.com/weihai-limh/llm_reasoning_world_twin/blob/main/document/image/llm_reasoning_world_twin_flowchart.png)
## prompt
<br>用户的初始提问经过'prompt_agent'转化为包含'base_guided','base_guided',
<br>'base_guided','base_guided'的'prompt'
<br>将'prompt'提交模型进行推理后既可得到基于'数字孪生'及'相关规则'的推理结果
<br>生成推理结果后可以使推理结果继续在'数字孪生'环境中继续驱动其他行为.
```
from openai import OpenAI 
modle_obj = {
	'api_key':'api_key',
	'base_url':'base_url',
	'model_name':'model_name',
}
def get_inference_results(inference_object,modle_obj):
	client = OpenAI(
	    api_key=modle_obj['api_key'],
	    base_url=modle_obj['base_url'],
	) 
	completion = client.chat.completions.create(
	    model=modle_obj['model_name'],  
	    messages=inference_object,
	    top_p=0.7,
	    temperature=0.9
	 ) 
	 rst = completion.choices[0].message
 	return rst

base_inference_object=[    
	{"role": "system", "content": "<base_guided>"},   #<base_guided>是基于数字孪生模型的基础规则
	{"role": "user", "content": "<business_rules>"},    #<business_rules>是基于'问题'召回的'业务规则'
	{"role": "user", "content": "<user_problems>"},   #<user_problems>是用户的初始提问
	{"role": "user", "content": "<text_expression_of_digital_twins>"}    #<text_expression_of_digital_twins>是以文本描述的对应数字孪生描述的相关内容
]

BDDATA = '{"2qCeoFbPb859$FJjqUkKC9": {"name": "29", "type": "IfcSpace", "BuildingStorey": "F7", "area": "13.00m²", "LongName": "办公室c", "spatial_rel": ["2qCeoFbPb859$FJjqUkKCD", "2qCeoFbPb859$FJjqUkKBl"]}, "2qCeoFbPb859$FJjqUkKCD": {"name": "30", "type": "IfcSpace", "BuildingStorey": "F7", "area": "7.25m²", "LongName": "休息室", "spatial_rel": ["2qCeoFbPb859$FJjqUkKC9"]}, "2qCeoFbPb859$FJjqUkKBo": {"name": "31", "type": "IfcSpace", "BuildingStorey": "F7", "area": "14.50m²", "LongName": "会议室", "spatial_rel": ["2qCeoFbPb859$FJjqUkKBt"]}, "2qCeoFbPb859$FJjqUkKBt": {"name": "32", "type": "IfcSpace", "BuildingStorey": "F7", "area": "9.57m²", "LongName": "办公室a", "spatial_rel": ["2qCeoFbPb859$FJjqUkKB_", "2qCeoFbPb859$FJjqUkKBo"]}, "2qCeoFbPb859$FJjqUkKBq": {"name": "33", "type": "IfcSpace", "BuildingStorey": "F7", "area": "8.99m²", "LongName": "办公室f", "spatial_rel": ["2qCeoFbPb859$FJjqUkKB_"]}, "2qCeoFbPb859$FJjqUkKBv": {"name": "34", "type": "IfcSpace", "BuildingStorey": "F7", "area": "11.02m²", "LongName": "办公室i", "spatial_rel": ["2qCeoFbPb859$FJjqUkKB_"]}, "2qCeoFbPb859$FJjqUkKB_": {"name": "35", "type": "IfcSpace", "BuildingStorey": "F7", "area": "24.94m²", "LongName": "大厅", "spatial_rel": ["2qCeoFbPb859$FJjqUkKBl", "2qCeoFbPb859$FJjqUkKBi", "2qCeoFbPb859$FJjqUkKBt", "2qCeoFbPb859$FJjqUkKBq", "2qCeoFbPb859$FJjqUkKBv", "2qCeoFbPb859$FJjqUkKBZ", "2qCeoFbPb859$FJjqUkKBb", "2qCeoFbPb859$FJjqUkKBg"]}, "2qCeoFbPb859$FJjqUkKBZ": {"name": "36", "type": "IfcSpace", "BuildingStorey": "F7", "area": "5.22m²", "LongName": "备品间", "spatial_rel": ["2qCeoFbPb859$FJjqUkKB_"]}, "2qCeoFbPb859$FJjqUkKBW": {"name": "37", "type": "IfcSpace", "BuildingStorey": "F7", "area": "4.68m²", "LongName": "机房", "spatial_rel": ["2qCeoFbPb859$FJjqUkKBb"]}, "2qCeoFbPb859$FJjqUkKBb": {"name": "38", "type": "IfcSpace", "BuildingStorey": "F7", "area": "8.32m²", "LongName": "办公室d", "spatial_rel": ["2qCeoFbPb859$FJjqUkKB_", "2qCeoFbPb859$FJjqUkKBW"]}, "2qCeoFbPb859$FJjqUkKBg": {"name": "39", "type": "IfcSpace", "BuildingStorey": "F7", "area": "8.58m²", "LongName": "办公室e", "spatial_rel": ["2qCeoFbPb859$FJjqUkKB_"]}, "2qCeoFbPb859$FJjqUkKBl": {"name": "40", "type": "IfcSpace", "BuildingStorey": "F7", "area": "4.42m²", "LongName": "办公室b", "spatial_rel": ["2qCeoFbPb859$FJjqUkKB_", "2qCeoFbPb859$FJjqUkKC9"]}, "2qCeoFbPb859$FJjqUkKBi": {"name": "41", "type": "IfcSpace", "BuildingStorey": "F7", "area": "6.67m²", "LongName": "高区楼梯间", "spatial_rel": ["2qCeoFbPb859$FJjqUkKB_"]}}'

inference_object=[    
    {"role": "system", "content": "Obtain data from the user's bd_data to answer;Don't reply to codes only return inference;Returns results only in json format, where json's key is \'rst\'"},   
    {"role": "user", "content": ''},   
    {"role": "user", "content": "I need to get from the computer room to the lounge"}, 
    {"role": "user", "content": "bd_data="+BDDATA}
]
print(get_inference_results(inference_object,modle_obj))
```
### 数字孪生描述
<br>'数字孪生描述'本质是语义统一的描述,但是为了在现实中各个领域有更好的应用
<br>我依然对其按应用场景进行分类
![digital_twins_description_types](https://github.com/weihai-limh/llm_reasoning_world_twin/blob/main/document/image/digital_twins_description_types_cn.png)
<br>**空间数字孪生描述**:
<br>现实中绝大多数活动都受其发生的现实空间所影响,
<br>'空间数字孪生描述'即是以文本形式对真实世界所在环境的语义表达,
<br>'空间数字孪生描述'的数据源可自行生产或从政府的开放数据中得到.
<br>我在数据源接入上主要以*.ifc(.usd),*.geojson(.osgb/.splat)为主,
<br>在基于推理生成的结果中,可以通过'图形引擎'对'空间数字孪生描述'模型进行物理模拟及可视化表达.
<br>可以根据喜好选用开源或商用的图形引擎,继续完成基础的物理模拟及相关的可视化表达.
<br>**人体数字孪生描述**:
<br>除空间之外,身体也很重要,
<br>与'空间'相仿我们可以通过ai对'人体的数字孪生描述'及遇到的问题进行推理,
<br>并用图形引擎进行模拟与可视化表达.'人体数字孪生描述'主要由:
<br>'可视化人体数据集','人体三维模型','人体器官语义描述'构成,
<br>通过基于'人体器官语义描述'的推理将结果映射到'可视化人体数据集'及'人体三维模型'
<br>**风帆航海数字孪生描述**:
<br>'风帆航海相关的数字孪生描述'是基于'空间相关的数字孪生描述'的进一步表达,
<br>该语义支持空间管理外还支持'风帆航海'相关的特定语义,补充了'迎风转向','顺风转向'等特定领域的行为
<br>**水肺潜水数字孪生描述**:
<br>'潜水相关的数字孪生描述'与'风帆航海相关的数字孪生描述'类似,
<br>基于'人体相关的数字孪生描述'补充了'检查装备'等24项技巧对应的特定领域的行为特定领域行为
### 空间数字孪生描述
<br>在'空间数字孪生描述'中我构建了两种描述,一种是用于和时序数据结合的'运维空间数字孪生描述',
<br>另一种是用于检修隐蔽工程或对应数字建造的'工程空间数字孪生描述'
<br>以下为空间运维的'空间数字孪生描述'的结构示例
```
{
	"2qCeoFbPb859$FJjqUkKCD": {
		"name": "",    
		"type": "IfcSpace",    #实例类型
		"BuildingStorey": "F7",    #实例所在楼层
		"area": "7.25m²",    #实例属性'面积'
		"LongName": "休息室",    #实例属性'空间代称'
		"spatial_rel": ["2qCeoFbPb859$FJjqUkKC9"]    #与其相联通的实例空间
	},
	"25O0a6_Pv35fvqlZsVbcJ1": {"name": "基本墙:常规 - 200mm:213408", "type": "IfcWall", "BuildingStorey": "F6"},
    "uuid_container_0201":  #容器名称
    {
        "described":"",     #容器描述
        "modle":"savs07",   #容器所属场景
        "room":"小商铺_F1",    #容器所属空间
        "location_data":"20240808",     #容器变更时间
        "base_component":"",      #容器对应的几何模型(当'geo_types'为'openusd')的引用地址
        "geo_types":"new_geo",      #容器的几何类型
        "basic_size":["box", 0.25, 0.25, 0.25],      #当'geo_types'为'new_geo'时,对容器的几何描述
        "translate":[-150.8052770040327, -81.62522162938637, 99.66055211222924],    #几何模型场景内定位
        "rotateXYZ":[-150.8052770040327, -81.62522162938637, 99.66055211222924],    #几何模型位置的角度
        "scale":[-150.8052770040327, -81.62522162938637, 99.66055211222924],    #几何模型缩放
        "nearest_location":{    #上一个位置
            "data":"20240805",    #上一个位置的时间
            "room":"大厅_F1",     #上一个位置的所属空间
            "translate":[-150.8052770040327, -81.62522162938637, 99.66055211222924] #上一个位置的场景内定位
        }
    },
    "uuid_container_0202":
    {
        "described":"",
        "modle":"savs07",
        "room":"办公室3_F2",
        "location_data":"20240808",
        "base_component":"<path>",
        "geo_types":"openusd",
        "basic_size":"",
        "translate":[-150.8052770040327, -81.62522162938637, 99.66055211222924],
        "rotateXYZ":[-150.8052770040327, -81.62522162938637, 99.66055211222924],
        "scale":[-150.8052770040327, -81.62522162938637, 99.66055211222924],
        "nearest_location":{}
    }
	"uuid_68200036":{
        "name":"跨领域信息交互方法与技术",  #资产实例的代称
        "types":"books",     #资产类型
        "container":"uuid_96300002"     #资产所在容器
    },
    "uuid_75400092":
    {
        "name":"","types":"clothes","container":"uuid_96300001"
    }
}
```
#### 数据转化
<br>'空间数字孪生描述'的属性描述基于IFC(ISO 16739-1:2018),
<br>将IFC文件通过转化工具将其转化为以guid为key的属性描述文后即可将其做为基础的'空间数字孪生描述'.
<br>如需对推理得到的结果进行可视化展示或对推理内容进行物理模拟则还需要将*.ifc文件转化出带guid的gltf文件.
<br>实践中可自行通过开源或商用的'转化工具'或自研完成相关的数据转化工作.
<br>如果源数据为.osgb/.splat等通过影像得到的三维重建对象,亦可通过.ifc/.geojson完成数据标定后转化为'空间数字孪生描述'
![data_conversion](https://github.com/weihai-limh/llm_reasoning_world_twin/blob/main/document/image/data_conversion.png)
### 人体数字孪生描述
<br>基础的'人体数字孪生描述'详见
<br>以下为基础的'人体数字孪生描述'的结构示例
```
{
    {
        "name": "Body",     #名词
        "type": "Body",     #类型
        "parent_class": "null",     #父级
        "chinese_description": "身体轮廓",     #中文描述
        "base_entity": "false"     #是否具有实体
    },
    {
        "name": "Cardiovascular",
        "type": "Cardiovascular",
        "parent_class": "null",
        "chinese_description": "心血管系统",
        "base_entity": "false"
    },
    {
        "name": "Heart",
        "type": "Cardiovascular",
        "parent_class": "Cardiovascular",
        "chinese_description": "心",
        "base_entity": "true"
    },
    {
        "name": "Eyes",
        "type": "Nervous;Central",
        "parent_class": "Central",
        "chinese_description": "眼睛",
        "base_entity": "false"
    },
    {
        "name": "Optic_Chiasm",
        "type": "Nervous;Central;Eyes",
        "parent_class": "Eyes",
        "chinese_description": "视交叉",
        "base_entity": "true"
    },
    {
        "name": "Cornea_L",
        "type": "Nervous;Central;Eyes",
        "parent_class": "Eyes",
        "chinese_description": "角膜_左",
        "base_entity": "true"
    }
}
```
<br>以下为基础的'可视化人体数据集'的结构示例
```
```
## 跨模态数据融合
<br>'数字孪生描述'基于'构式句法'等机制实现跨模态数据融合.
<br>将文本语义(业务规则),三维几何(空间结构),时序数据(IoT传感器)统一为机器可理解的数字孪生对象.
<br>并以此体高推理结果的可用性.并可通过'图技术'不断体高'数字孪生描述'的可靠程度
## 推理结果结合'图形引擎'及IOT实现'空间智能'
<br>该项目的内容为'通过大语言模型对现实世界的数字孪生对象进行推理',
<br>推理后通过和'图形引擎'与IOT的联合可以实现一定程度的空间智能.
<br>其得以实现的关键点在于通过对接的IOT监听'事件',
<br>当发生事件后将事件转化为'user_problems'激活项目生成推理结果,
<br>当生成推理结果后,将生成的内容转化为'数字孪生对象'的属性更新.
<br>当'数字孪生对象'的属性更新后将更新同步到加载'数字孪生对象'的'图形引擎',
<br>'图形引擎'对新的'属性文件'进行解析,并从解析中判断是否有要执行的'指令',
<br>如有则执行指令,该指令通过restful API驱动IOT设备在现实空间中执行动作,
<br>如改变现实空间中对象的位置,则进一步触发修改指令,更新数字孪生对象的'几何文件'
![inference_result2spatial_Intelligence](https://github.com/weihai-limh/llm_reasoning_world_twin/blob/main/document/image/inference_result2spatial_Intelligence_cn.png)

## 应用示例
### 空间数字孪生描述
对'空间数字孪生描述'的推理主要解决与空间相关的问题
<br>查找房间中的某项物品:
```
user_problems = 'How many coffee capsules are there in the lounge?' #休息室还有多少咖啡胶囊
business_rules = 'The returned content must contain the container identification, and the key of the identification is guid' #返回的内容必须包含容器标识,标识的key是guid
BDDATA = '{"2qCeoFbPb859$FJjqUkKC9": {"name": "29", "type": "IfcSpace", "BuildingStorey": "F7", "area": "13.00m²", "LongName": "办公室c", "spatial_rel": ["2qCeoFbPb859$FJjqUkKCD", "2qCeoFbPb859$FJjqUkKBl"]}, "2qCeoFbPb859$FJjqUkKCD": {"name": "30", "type": "IfcSpace", "BuildingStorey": "F7", "area": "7.25m²", "LongName": "休息室", "spatial_rel": ["2qCeoFbPb859$FJjqUkKC9"]},"uuid_container_0712":{"described":"","modle":"savs07","room":"休息室_F7", "location_data":"20240808","base_component":"","geo_types":"openusd","basic_size":"","translate":[-150.8052770040327, -81.62522162938637, 99.66055211222924],"rotateXYZ":[-150.8052770040327, -81.62522162938637, 99.66055211222924],"scale":[1, 1, 1],"nearest_location":{}},"uuid_79200178":{name":"咖啡胶囊", "count":"5","types":"snacks","container":"uuid_container_0712"}}'
inference_object=[    
    {"role": "system", "content": "Obtain data from the user's bd_data to answer;Don't reply to codes only return inference;Returns results only in json format, where json's key is \'rst\'"},   
    {"role": "user", "content": business_rules},   
    {"role": "user", "content": user_problems}, 
    {"role": "user", "content": "bd_data="+BDDATA}
]
```
<br>获得推理结果('物品'在空间中的位置)后,
<br>通过对数字孪生对象的修改自动激活与'图形引擎'的交互,并自动调用'室内导航'微服务,通过该服务生成'室内导航'
<br>除'查找房间中的某项物品'外还可以通过该方法'结合知识预测空间能否满足某些规则';
<br>还可以快速定位建筑物内的隐蔽工程,例如'建筑中的水管或电线'
<br>获得推理结果后,可以自动激活与'图形引擎'的交互,并自动'高亮显示'推理结果中符合条件的'数字孪生对象'对应的'几何模型'.
<br>除此自外还可以基于该方法在在'房间内布置新的家家具'或'基于空间生成新的装修方案'
<br>获得推理结果后,可以自动激活与'图形引擎'的交互,并自动调用'生成几何对象'微服务,在图形引擎的渲染场景中追加渲染新增的'数字孪生对象'的'几何模型'
### 人体数字孪生描述
<br>查看器官及其周围的器官
```
user_problems = 'Looking at the 2-degree relationship of the heart in the cardiovascular and digestive systems' #在心血管系统和消化系统中查看心的2度关系
business_rules = 'Only the contents of the cardiovascular system and digestive system participate in reasoning.The returned content must contain the container identification, and the key of the identification is name'
HBDATA = '<数据见前文'人体数字孪生描述'>'
inference_object=[    
    {"role": "system", "content": "Obtain data from the user's hb_data to answer;Don't reply to codes only return inference;Returns results only in json format, where json's key is \'rst\'"},   
    {"role": "user", "content": business_rules},   
    {"role": "user", "content": user_problems}, 
    {"role": "user", "content": "hb_data="+HBDATA}
]
```
<br>获得推理结果后,可以自动激活与'图形引擎'的交互,在图形引擎的渲染场景中追加渲染新增的'数字孪生对象'的'几何模型'
<br>除器官查看外还可以与'可视化人体数据集'进行联动
<br>获得推理结果后,可以自动激活与'可视化人体数据集'的交互,并自动在交互页面中显示'数字孪生对象'对应的'CT'影像及影像注记
## 其他
### 可信度
<br>在日常使用中我通过'antlr4'及'neo4j'对推理结果后续的应用进行管控,
<br>例如通过图查询校验关于'室内空间导航'的相关问题.
### 价值
<br>我自在现实中应用这个范式感受到了它带来的价值,所以愿意分享它.
<br>希望有更多的人能够通过它改善'生活体验'享受到人工智能带来的便利.
<br>该领域相关技术的应用过去主要用于B端及G端,
<br>过去难以推广的关键原因是过去需要大量的人在数字孪生的基础上结合行业知识开发应用.
<br>现在结合LLMs相关技术实现了'ai生成数字孪生对象的应用',由此可以满足更多用户对空间的想象.
<br>在产品与用户的交互层面,由于实现了'大语言模型对数字孪生对象'的推理,并以端渲染为用户提供免费的基于现实场景的'三维可视化表达'
<br>但是让使用者更明确的感受到'它带给使用者'的价值,还需要向其提供更精确的时效性更强的'数字孪生对象'
### 未来
<br>过去一年基于'LLM的推理能力',进行多种领域模型的'跨模态数据融合'和数据治理.
<br>与图形引擎集成,通过restful API驱动IOT设备我基于'推理结果'的应用边界上进行了大量的是错.
<br>并最终确定了'推理结果'确实可以通过驱动'数字孪生场景'在现实中实现更多价值.
<br>一个人凭着热爱冲不动了,后面不会单凭自己全职投入了,后面看情况慢慢更新吧.

