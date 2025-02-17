# llm_reasoning_world_twin
<br>Use LLM to reason the digital twin model and use it as the 'digital twin hub' to drive IOT, thereby solving problems related to it in reality
<br>[中文](https://github.com/weihai-limh/llm_reasoning_world_twin/blob/main/document/docs/README_CN.md)
<br>The digital twin object is an aggregate comprising semantic description files and geometric files.  
<br>The project leverages large language models (LLMs) to reason about real-world digital twin objects.  
<br>Since the reasoning results include digital twin objects, they can be simulated using a graphics engine.  
<br>These results are then projected into the real world via IoT, enabling the execution of the inferred outcomes.  
![llm_reasoning_flowchart](https://github.com/weihai-limh/llm_reasoning_world_twin/blob/main/document/image/llm_reasoning_world_twin_flowchart.png)

## Prompt  
<br>The user's initial query is processed by the **Prompt Agent** to generate a structured **prompt** containing **base_guided**, **base_guided**, **base_guided**, and **base_guided**.  
<br>Submitting this **prompt** to the model for inference yields results grounded in **digital twin** logic and **relevant rules**.  
<br>Once generated, these reasoning outcomes can further drive additional behaviors within the digital twin environment.  

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
	{"role": "system", "content": "<base_guided>"},   #<base_guided>are based on the basic rules of the digital twin model
	{"role": "user", "content": "<business_rules>"},    #<business_rules>Is a 'business rule' based on a 'problem' recall
	{"role": "user", "content": "<user_problems>"},   #<user_problems>Is the user's initial question
	{"role": "user", "content": "<text_expression_of_digital_twins>"}    #<text_expression_of_digital_twins>It is a text description corresponding to the corresponding digital twin description
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


### Digital Twin Descriptions  
<br>**Digital Twin Descriptions** are inherently unified semantic representations. However, to better apply them across real-world domains,  
<br>they are categorized by application scenarios.  
[Diagram: Types of Digital Twin Descriptions]  

<br>**Spatial Digital Twin Description**:  
<br>The majority of real-world activities are influenced by their physical environments.  
<br>The **Spatial Digital Twin Description** is a textual semantic representation of real-world environments.  
<br>Data sources for this description can be self-generated or obtained from government open-data repositories.  
<br>For data integration, formats such as `*.ifc` (or `.usd`), `*.geojson` (or `.osgb`/`.splat`) are prioritized.  
<br>Inference-generated results can leverage **graphics engines** to perform physical simulations and visualizations of spatial digital twin models.  
<br>Open-source or commercial graphics engines may be selected based on preference to execute basic simulations and visualizations.  

<br>**Human Body Digital Twin Description**:  
<br>Beyond spatial contexts, the human body is equally critical.  
<br>Similar to spatial descriptions, AI can reason about **Human Body Digital Twin Descriptions** and associated challenges,  
<br>then simulate and visualize them via graphics engines. This description comprises:  
<br>- **Visualized human datasets**  
<br>- **3D human models**  
<br>- **Semantic descriptions of human organs**  
<br>Reasoning based on **semantic organ descriptions** maps results to visualized datasets and 3D models.  

<br>**Sailing Navigation Digital Twin Description**:  
<br>The **Sailing Navigation Digital Twin Description** extends spatial descriptions with domain-specific semantics for sailing.  
<br>In addition to spatial management, it supports sailing-specific behaviors such as **tacking** and **jibing**.  

<br>**Scuba Diving Digital Twin Description**:  
<br>Similar to sailing descriptions, the **Scuba Diving Digital Twin Description** builds on human body descriptions,  
<br>adding 24 domain-specific techniques (e.g., **equipment checks**) and related behavioral semantics.  

### Spatial Digital Twin Description  
<br>Within **Spatial Digital Twin Descriptions**, I have constructed two types of descriptions:  
1. **Operational Spatial Digital Twin Description**: Designed to integrate with time-series data for facility management.  
2. **Engineering Spatial Digital Twin Description**: Used for inspecting concealed engineering systems or digital construction.  

<br>Below is a structural example of an **Operational Spatial Digital Twin Description**:  

```
{
	"2qCeoFbPb859$FJjqUkKCD": {
		"name": "",    
		"type": "IfcSpace",    #Object instance type
		"BuildingStorey": "F7",    #Floor where the object instance is located
		"area": "7.25m²",    #Object instance attribute 'Area'
		"LongName": "休息室",    #The 'spatial proxy' of the object instance attribute to the specific space
		"spatial_rel": ["2qCeoFbPb859$FJjqUkKC9"]    #The space where an object instance connects with other object instances
	},
	"25O0a6_Pv35fvqlZsVbcJ1": {"name": "基本墙:常规 - 200mm:213408", "type": "IfcWall", "BuildingStorey": "F6"},
    "uuid_container_0201":  #Identity of the container when the object instance is a container
    {
        "described":"",     #container description
        "modle":"savs07",   #Building to which the container belongs
        "room":"小商铺_F1",    #Space to which container belongs
        "location_data":"20240808",     #Container position change time
        "base_component":"",      #The reference address of the geometric model corresponding to the container (when 'geo_types' is 'openusd')
        "geo_types":"new_geo",      #Type of container geometry object
        "basic_size":["box", 0.25, 0.25, 0.25],      #The geometric description of the container when 'geo_types' is 'new_geo'
        "translate":[-150.8052770040327, -81.62522162938637, 99.66055211222924],    #Geometric model positioning in building
        "rotateXYZ":[-150.8052770040327, -81.62522162938637, 99.66055211222924],    #Geometric model angle
        "scale":[-150.8052770040327, -81.62522162938637, 99.66055211222924],    #Geometric model scaling
        "nearest_location":{    #to a location on a
            "data":"20240805",    #Time at previous location
            "room":"大厅_F1",     #Space of previous location
            "translate":[-150.8052770040327, -81.62522162938637, 99.66055211222924] #In-building positioning of previous location
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
        "name":"跨领域信息交互方法与技术",  #Proxy name for asset instance
        "types":"books",     #Asset instance type
        "container":"uuid_96300002"     #Container in which the asset is located
    },
    "uuid_75400092":
    {
        "name":"","types":"clothes","container":"uuid_96300001"
    }
}
```
#### Data Transformation  
<br>The attribute descriptions of **Spatial Digital Twin Descriptions** are based on IFC (ISO 16739-1:2018).  
<br>By using conversion tools, IFC files can be transformed into attribute description files with **guid** as the key, which then serve as the foundational **Spatial Digital Twin Descriptions**.  
<br>To visualize the inferred results or perform physical simulations, the `*.ifc` files must also be converted into **glTF** files containing **guid**.  
<br>In practice, this data transformation can be achieved using open-source or commercial **conversion tools**, or through custom-developed solutions.  
<br>If the source data consists of 3D reconstructed objects (e.g., `.osgb` or `.splat`) derived from imagery, they can also be calibrated using `.ifc` or `.geojson` and then transformed into **Spatial Digital Twin Descriptions**. 

[数据转化]()


### Human Body Digital Twin Description  
<br>For the foundational **Human Body Digital Twin Description**, please refer to the details below.  
<br>Here is a structural example of the foundational **Human Body Digital Twin Description**:  

```
{
    {
        "name": "Body",     #special term
        "type": "Body",     #hierarchy type
        "parent_class": "null",     #parent class
        "chinese_description": "身体轮廓",     #Proprietary description in Chinese
        "base_entity": "false"     #Whether it is an entity
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
<br>The following is an example of the structure of a 'visualized human dataset' based on
```
```

## Cross-Modal Data Fusion  
<br>**Digital Twin Descriptions** achieve cross-modal data fusion through mechanisms such as **constructional syntax**.  
<br>This unifies textual semantics (business rules), 3D geometry (spatial structures), and time-series data (IoT sensors) into machine-understandable digital twin objects.  
<br>This enhances the usability of inference results and continuously improves the reliability of **Digital Twin Descriptions** through **graph technologies**.  

## Combining Inference Results with **Graphics Engines** and IoT to Achieve **Spatial Intelligence**  
<br>The core of this project is **"reasoning about real-world digital twin objects using large language models"**.  
<br>By integrating **graphics engines** and IoT, a certain level of **spatial intelligence** can be achieved.  
<br>The key to its implementation lies in listening to **events** through connected IoT systems.  
<br>When an event occurs, it is transformed into **user_problems**, triggering the project to generate inference results.  
<br>Once the inference results are generated, they are converted into updates to the attributes of the **digital twin objects**.  
<br>After updating the attributes of the **digital twin objects**, the changes are synchronized with the **graphics engine** that loads these objects.  
<br>The **graphics engine** parses the new **attribute files** and determines whether there are any **instructions** to execute.  
<br>If instructions exist, they are executed via RESTful APIs, driving IoT devices to perform actions in the physical space.  
<br>For example, if the position of an object in the physical space is changed, this triggers further update instructions, modifying the **geometry files** of the digital twin objects.  

[综合图]()


## Application Examples  
### Spatial Digital Twin Description  
Reasoning with **Spatial Digital Twin Descriptions** primarily addresses space-related issues.  
<br>Example: Locating a specific item in a room.  

```
user_problems = 'How many coffee capsules are there in the lounge?' 
business_rules = 'The returned content must contain the container identification, and the key of the identification is guid' 
BDDATA = '{"2qCeoFbPb859$FJjqUkKC9": {"name": "29", "type": "IfcSpace", "BuildingStorey": "F7", "area": "13.00m²", "LongName": "办公室c", "spatial_rel": ["2qCeoFbPb859$FJjqUkKCD", "2qCeoFbPb859$FJjqUkKBl"]}, "2qCeoFbPb859$FJjqUkKCD": {"name": "30", "type": "IfcSpace", "BuildingStorey": "F7", "area": "7.25m²", "LongName": "休息室", "spatial_rel": ["2qCeoFbPb859$FJjqUkKC9"]},"uuid_container_0712":{"described":"","modle":"savs07","room":"休息室_F7", "location_data":"20240808","base_component":"","geo_types":"openusd","basic_size":"","translate":[-150.8052770040327, -81.62522162938637, 99.66055211222924],"rotateXYZ":[-150.8052770040327, -81.62522162938637, 99.66055211222924],"scale":[1, 1, 1],"nearest_location":{}},"uuid_79200178":{name":"咖啡胶囊", "count":"5","types":"snacks","container":"uuid_container_0712"}}'
inference_object=[    
    {"role": "system", "content": "Obtain data from the user's bd_data to answer;Don't reply to codes only return inference;Returns results only in json format, where json's key is \'rst\'"},   
    {"role": "user", "content": business_rules},   
    {"role": "user", "content": user_problems}, 
    {"role": "user", "content": "bd_data="+BDDATA}
]
```
<br>After obtaining the inference result (the location of the **item** in the space),  
<br>modifications to the digital twin object automatically trigger interactions with the **graphics engine** and invoke the **indoor navigation** microservice. This service generates an **indoor navigation** path.  
<br>In addition to **locating a specific item in a room**, this method can also **predict whether a space can satisfy certain rules based on knowledge**.  
<br>It can also quickly locate concealed engineering systems within a building, such as **water pipes or electrical wires**.  
<br>Once the inference result is obtained, interactions with the **graphics engine** are automatically activated, and the corresponding **geometric models** of the qualified **digital twin objects** in the inference result are **highlighted**.  
<br>Beyond this, the method can also be used to **arrange new furniture in a room** or **generate new renovation plans based on the space**.  
<br>After obtaining the inference result, interactions with the **graphics engine** are automatically activated, and the **generate geometric object** microservice is invoked to render and add the **geometric models** of the newly created **digital twin objects** in the graphics engine's scene.  

### Human Body Digital Twin Description  
<br>View an organ and its surrounding organs. 
```
user_problems = 'Looking at the 2-degree relationship of the heart in the cardiovascular and digestive systems' 
business_rules = 'Only the contents of the cardiovascular system and digestive system participate in reasoning.The returned content must contain the container identification, and the key of the identification is name'
HBDATA = '<See the previous article 'Human Digital Twin Description>'
inference_object=[    
    {"role": "system", "content": "Obtain data from the user's hb_data to answer;Don't reply to codes only return inference;Returns results only in json format, where json's key is \'rst\'"},   
    {"role": "user", "content": business_rules},   
    {"role": "user", "content": user_problems}, 
    {"role": "user", "content": "hb_data="+HBDATA}
]
```

<br>After obtaining the inference result, interactions with the **graphics engine** are automatically activated, and the **geometric models** of the newly created **digital twin objects** are rendered and added to the graphics engine's scene.  
<br>In addition to organ visualization, this can also be integrated with **visualized human datasets**.  
<br>Once the inference result is obtained, interactions with the **visualized human dataset** are automatically triggered, and the corresponding **CT images** and annotations of the **digital twin objects** are displayed on the interactive interface.  

## Other  
### Credibility  
<br>In daily use, I manage the subsequent applications of inference results through **ANTLR4** and **Neo4j**.  
<br>For example, graph queries are used to validate issues related to **indoor space navigation**.  

### Value  
<br>Having applied this paradigm in real-world scenarios, I have experienced its value firsthand and am eager to share it.  
<br>I hope more people can use it to improve their **life experiences** and enjoy the convenience brought by artificial intelligence.  
<br>In the past, related technologies in this field were primarily used in **B2B** and **B2G** contexts.  
<br>The main barrier to widespread adoption was the need for extensive human effort to develop applications by combining industry knowledge with digital twin foundations.  
<br>Now, with the integration of **LLM-related technologies**, **AI-generated applications of digital twin objects** have become possible, fulfilling more users' imaginations of space.  
<br>At the product-user interaction level, by enabling **large language models to reason about digital twin objects** and providing users with free **3D visualizations** of real-world scenarios through client-side rendering,  
<br>users can better perceive the value it brings. However, to make this value even clearer, more precise and timely **digital twin objects** need to be provided.  

### Future  
<br>Over the past year, leveraging the **reasoning capabilities of LLMs**, I have conducted **cross-modal data fusion** and data governance across various domain models.  
<br>By integrating with graphics engines and driving IoT devices via RESTful APIs, I have extensively explored the application boundaries of **inference results**.  
<br>Ultimately, I confirmed that **inference results** can indeed drive **digital twin scenarios** to create more value in the real world.  
<br>As one person, I can no longer push forward solely based on passion. Moving forward, it will be about work. I hope the right people can unlock its greater potential.  