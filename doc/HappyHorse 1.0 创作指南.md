# HappyHorse 1.0 创作指南

:::
✨ 为大家介绍由阿里巴巴-ATH 团队打造的 HappyHorse 1.0 视频生成模型及 HappyHorse 视频创作平台。

HappyHorse 1.0 依托原生多模态架构，采用音视频联合生成方案，面向广告、电商、短剧、社媒创意等内容生产场景，提供从智能生成到编辑的一体化创作能力。作为持续进化中的新一代视频生成模型，HappyHorse 1.0 在画面质感、镜头运动、人物真实感与内容可控性等方面，均已展现出较强的行业竞争力。

HappyHorse 1.0体验入口 👉 [https://www.happyhorse.cn/](https://www.happyhorse.cn/)    

API 申请入口  👉 [https://bailian.console.aliyun.com/](https://bailian.console.aliyun.com/cn-beijing?tab=model#/model-market/detail/happyhorse-1.0-t2v?serviceSite=asia-pacific-china)     
:::

# 核心功能

HappyHorse 1.0 目前支持两个核心功能：【多模态视频生成】和【视频编辑】。既能从 0 到 1 生成视频，也能对已有视频素材做从 1 到 N 的创意延展。

## 1.1 多模态视频生成

### 文生视频

通过文本描述生成视频。创作者只需输入文字提示词，描述期望的画面内容、风格和动态效果，即可生成对应的视频片段。适用于从零开始构思创意、快速验证想法等场景。

### 图生视频

以一张静态图片作为参考输入，生成与图片内容风格一致的动态视频。适用于将静态设计稿、插画、摄影作品等赋予动态效果的场景。

### 多图参考生视频

支持输入多张参考图片来引导视频生成。通过多张图片提供更丰富的视觉参考信息，让生成结果在角色一致性、场景连贯性或风格统一性上获得更精准的控制。适用于需要保持角色/元素一致性的叙事类创作等场景。

|  | **首帧图生视频** | **多图参考生视频** |
| --- | --- | --- |
| **图片作用** | 图片 = 视频第一帧画面，精确还原 | 图片 = 视觉参考素材，提取特征后融入视频 |
| **图片数量** | 1 张 | 1-9 张 |
| **图像还原度** | 极高，第一帧几乎与原图一致 | **主体参考：**模型会借鉴图像中的身份特征/视觉元素，但不会逐像素复制原图。**关键帧参考：**对每张参考图进行近像素级的高保真还原 |
| **画幅比例** | 跟随原图 | 可自由选择（16:9 / 9:16 等） |
| **分辨率** | 720P、1080P | 720P、1080P |
| **文本提示词** | 可选项 | 必选项 |
| **典型场景** | "基于这张分镜图，生成视频素材" | *   **主体参考：**"让@图1中的人骑着@图2中的马，在@图3的太空背景下奔驰"<br>    <br>*   **关键帧参考：**"以@图1作为第一个分镜，讲述一个关于XXX的故事；然后过渡到@图2作为下一个分镜，继续讲述XXX" |

## 1.2 视频编辑

支持对已有视频进行智能编辑，无需从零生成，在原片基础上实现精准修改。支持上传参考图进行视频编辑。

# 核心亮点

今天行业中每个视频模型都有自己擅长的领域，HappyHorse 1.0作为视频生成领域的新人，主要在**画面质感与光影效果、运镜与转场流畅度、面部/人物真实感**等方面有着优秀表现，HappyHorse也在持续进化，持续提升生成视频的质量和表现力。

## 2.1 电影级画面质感与光影表现

> _无论是人物肤质、发丝细节，还是金属反光、烟雾水雾等自然元素，HappyHorse 1.0均能呈现高度真实的视觉质感。_

[请至钉钉文档查看附件《案例视频.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mofjfz9xhlvx458bc6m&utm_medium=im_card&utm_scene=person_space&utm_source=im)

> _T2V Prompt：A cinematic script scene set in a sun-drenched Parisian café, golden afternoon light spilling through arched windows. A sharp-dressed man in a tailored navy suit sits across from an elegant woman in a flowing crimson dress, half-empty coffee cups between them. The air is thick with unspoken tension. He leans forward, voice low and steady: "You knew from the beginning, didn't you? That none of this was real." She holds his gaze without flinching, a ghost of a smile on her lips, slowly stirring her coffee: "Everything was real. That's exactly what makes it so dangerous."  Cinematic wide-angle composition, warm golden hour lighting, shallow depth of field, film grain texture, muted vintage color palette with deep crimson accents, highly detailed wardrobe and facial expressions, noir romantic aesthetic, emotionally charged atmosphere, European street photography style, dramatic storytelling, 35mm film look._

## 2.2 流畅稳定的运镜与转场能力

> _模型在镜头运动的连贯性和转场的自然度上表现优秀，支持拉近、拉远、景深变换等多种运镜方式，过渡丝滑，色调与环境融合连贯，能较好地遵循 prompt 中的镜头语言指令。_

[请至钉钉文档查看附件《HappyHorse-20260426-0002.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mofvc3khv8jvucqat5l&utm_medium=im_card&utm_scene=person_space&utm_source=im)

> _T2V Prompt：__纽约城市景观·超现实主义FPV一镜到底镜头脚本_

> _镜头从紧贴地面的极低角度猛然弹射而出，沿清晨无人的曼哈顿街头疾速贴地飞行。两侧褐石建筑、红砖楼宇化作流动色块，柏油路面的裂缝折射晨光，偶尔掠过的铸铁护栏、街头消防栓留下模糊残影。摄像机保持离地30厘米，每秒数米冲刺，轻微横向摇摆模拟手持呼吸感，悬铃木枝叶间隙的晨光形成连续光斑扫掠，落在复古的金属门牌号上。接近街角Bagel店时，镜头减速滑行、缓缓抬升，以弧线绕过第一张金属折叠桌，不锈钢面包篮的纹路掠过画面边缘。推进至Bagel店摊位深处，运动转为慢动作凝滞，以毫米级速度爬行，围绕悬浮的水流形成的文字 “HappyHorse 1.0”、冰美式咖啡、《纽约邮报》、Bagel面包等物品。镜头推至文字前方 15 厘米处静止凝视，液态文字微微涌动。瞬间，文字爆裂成无数水珠，摄像机被气浪猛推，急速后拉并向下俯冲，轨迹呈剧烈J形转折。镜头以自由落体砸向地面，触地前一帧再次突变，贴地超低空滑行，视角侧倾近 90度，右侧红砖建筑立面垂直耸立，街头黄色出租车的轮胎在视野边缘飞速后退。滑行两秒后，镜头向上弹射，沿曼哈顿摩天大楼（帝国大厦旁）外墙垂直爬升，仰角从水平转为垂直向上，玻璃幕墙反射的晨光形成连续光带，映出远处自由女神像的剪影。爬升至屋顶高度，外翻越过天台围栏，空中完成180 度轴向翻转，从仰望天空转为俯视深渊，沿世贸中心双子塔遗址周边高楼间的狭窄天井垂直下坠。下坠初始速度适中，镜头朝下稳定俯拍，天井四壁如方形画框向中心收缩，下方第五大道的车流化作彩色光轨。速度逐渐加快，镜头加入左右摆动，时而贴近布鲁克林红砖建筑擦过复古空调外机，时而摆向写字楼混凝土横梁，轨迹呈失控螺旋下坠。每经过一层平台，镜头随机偏转，仿佛被气流撞击，在狭窄空间中不断反弹、修正、偏离，偶尔掠过悬挂的霓虹招牌与街头涂鸦。下坠至中段，光线急剧衰减，虚拟暗光增强捕捉到老旧楼宇剥落的墙面、锈蚀的消防管道、杂乱的电缆。镜头开始沿光轴 360 度连续翻滚，天井四壁（一边是现代玻璃幕墙，一边是布鲁克林红砖墙）化作旋转的红与银的漩涡，偶尔闪现的Bagel店暖光、街头路灯如深渊中的孤岛。接近底部最后十米，速度极限，旋转平息，镜头重新垂直俯冲。即将撞击地面的瞬间，穿透无形镜面，重力方向倒置—从向下俯冲无缝切换为向上浮升，轨迹呈现莫比乌斯环式转折。进入镜像世界，镜头保持向前惯性，在倒置的纽约上空水平滑行。布鲁克林褐石屋、曼哈顿公寓屋顶群在脚下绵延至天际线，天空被踩在上方，两名倒悬的街头咖啡师（手持咖啡壶、吆喝声仿佛从天际传来）缓缓飘过。镜头优雅穿梭于漂浮的纸杯咖啡、牛皮纸袋与Bagel之间，做小幅升降起伏，围绕玻璃球缓慢椭圆运动，最终平稳直线推进，缓缓贴近玻璃球表面—球体中倒映的无限递归城市景观（第五大道、帝国大厦、布鲁克林大桥交织）逐渐填满画面，速度降至每秒不足一厘米，在绝对静止中淡出至纯白。_

[请至钉钉文档查看附件《HappyHorse-20260426-0008.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mofx3zw3grwqfd0gyb&utm_medium=im_card&utm_scene=person_space&utm_source=im)

> _T2V Prompt：羊毛毡风格·巴黎街道·超现实主义FPV一镜到底镜头脚本_

> _一镜到底，FPV 视角，超现实主义，羊毛毡质感。镜头从紧贴地面的极低角度猛然弹射而出，沿清晨无人的羊毛毡质感巴黎街道疾速贴地飞行。两侧浅米色羊毛毡缝制的石质建筑化作蓬松流动色块，羊毛毡铺就的电车轨道上，金属色羊毛线勾勒的凹槽泛着柔和冷光，针脚纹理清晰可见。摄像机保持离地30厘米，每秒数米冲刺，轻微横向摇摆模拟手持呼吸感，羊毛毡编织的树冠间隙，暖黄色羊毛毡光斑形成连续光带扫掠，落在毛茸茸的街道肌理上。接近街角羊毛毡咖啡座时，镜头减速滑行、缓缓抬升，以弧线绕过第一张羊毛毡缝制的圆桌，羊毛毡藤编椅背的绒面纹理掠过画面边缘，针脚缝隙里的绒毛清晰可辨。推进至咖啡座深处，运动转为慢动作凝滞，以毫米级速度爬行，围绕悬浮的羊毛毡质感水流（蓬松纤维模拟水流形态）形成的文字 “HappyHorse 1.0”、羊毛毡捏制的苹果、羊毛毡缝制的报纸等物品，所有物件均带着羊毛的蓬松弧度与柔和光泽。镜头推至文字前方 15 厘米处静止凝视，液态感的羊毛纤维文字微微涌动，绒毛随“气流”轻颤。瞬间，文字爆裂成无数蓬松羊毛碎屑与绒毛，摄像机被“气浪”猛推，急速后拉并向下俯冲，轨迹呈剧烈J形转折。镜头以自由落体砸向地面，触地前一帧再次突变，贴地超低空滑行，视角侧倾近 90度，右侧羊毛毡建筑立面垂直耸立，羊毛毡材质的白色货车轮胎在视野边缘飞速后退，轮胎纹理由粗细不一的羊毛线勾勒。滑行两秒后，镜头向上弹射，沿羊毛毡缝制的巴黎建筑外墙垂直爬升，仰角从水平转为垂直向上，羊毛毡模拟的玻璃幕墙反射着柔和光带，光带由渐变色彩的羊毛纤维组成，映出远处羊毛毡埃菲尔铁塔的迷你剪影。爬升至屋顶高度，外翻越过羊毛毡女儿墙，墙沿点缀着蓬松的羊毛绒球，空中完成180 度轴向翻转，从仰望天空转为俯视深渊，沿两栋羊毛毡高楼间的狭窄天井垂直下坠。_

> _下坠初始速度适中，镜头朝下稳定俯拍，天井四壁如方形羊毛毡画框向中心收缩，墙面布满均匀的针脚纹理。速度逐渐加快，镜头加入左右摆动，时而贴近羊毛毡红砖墙擦过羊毛缝制的空调格栅，格栅由细密羊毛线编织而成，时而摆向羊毛毡混凝土横梁，横梁表面有粗糙的羊毛肌理，轨迹呈失控螺旋下坠。每经过一层平台，镜头随机偏转，仿佛被气流撞击，在狭窄空间中不断反弹、修正、偏离，偶尔掠过悬挂的羊毛毡霓虹招牌（绒面色彩鲜明）与羊毛毡街头涂鸦。下坠至中段，光线急剧衰减，虚拟暗光增强捕捉到羊毛毡墙面“剥落”的绒毛、锈蚀质感的羊毛线管道、杂乱的羊毛绒电缆，所有破损细节均由不同色泽的羊毛纤维模拟，质感柔和不锐利。镜头开始沿光轴 360 度连续翻滚，天井四壁（一边是羊毛毡玻璃幕墙，一边是羊毛毡砖墙）化作旋转的柔和灰色漩涡，偶尔闪现的咖啡座暖光、羊毛毡路灯，如深渊中的毛茸茸孤岛，光线透过羊毛材质变得柔和朦胧。接近底部最后十米，速度极限，旋转平息，镜头重新垂直俯冲。即将撞击地面的瞬间，穿透无形镜面，重力方向倒置—从向下俯冲无缝切换为向上浮升，轨迹呈现莫比乌斯环式转折。进入镜像世界，镜头保持向前惯性，在倒置的羊毛毡巴黎上空水平滑行。羊毛毡巴黎屋顶群（覆盖着蓬松的羊毛“瓦片”）在脚下绵延至天际线，天空被踩在上方，两名倒悬的羊毛毡服务生（绒面质感，衣着色彩鲜艳）缓缓飘过，衣角的羊毛绒毛轻颤。镜头优雅穿梭于漂浮的羊毛毡咖啡杯、羊毛毡餐具之间，做小幅升降起伏，围绕羊毛毡玻璃球（表面覆盖薄绒，泛着柔和光泽）缓慢椭圆运动，最终平稳直线推进，缓缓贴近玻璃球表面—球体中倒映的无限递归羊毛毡城市景观（埃菲尔铁塔、塞纳河、巴黎街头交织）逐渐填满画面，速度降至每秒不足一厘米，在绝对静止中淡出至纯白，收尾处残留少许羊毛绒毛的朦胧质感。_

[请至钉钉文档查看附件《HappyHorse-20260426-0003.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mofthpfi84eubmy9oi9&utm_medium=im_card&utm_scene=person_space&utm_source=im)

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgXbNRG8RjlWN/img/79f29441-ab82-4c29-9e13-69765e630bc0.png)

> _I2V Prompt：跳舞，转了一圈后，从卡通变成现实场景。_

## 2.3 人物真实感强，面部表情有生命力

> _在人物面部细节的渲染上，HappyHorse 实现了重要突破。五官比例协调、面部轮廓自然、表情生动不僵硬，已基本摆脱传统 AI 生成视频中常见的"一眼假"感，在真人剧、口播、社媒等人物密集场景中表现亮眼_

[请至钉钉文档查看附件《例子2.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02moflabwbfuboxdj9nfa&utm_medium=im_card&utm_scene=person_space&utm_source=im)

> _T2V Prompt：【场景】冷白灯光打下的审讯室，金属桌面反光，烟灰缸里还有未熄的烟。 【主体】左侧【老刑警】西装褶皱，眼袋深重，手指慢慢敲着桌面；右侧【嫌疑人】双臂交叉，眼神游移，嘴角带着一丝不易察觉的轻蔑。 【运动】老刑警将一张照片缓缓推过桌面，嫌疑人眼神微微一顿又迅速移开；镜头低角度平推，捕捉两人手部与表情的细微对峙。 【音频】\[老刑警，语速极慢，每个字像钉子\]："你知道我做这行多少年了吗。" \[短暂沉默，烟灰缸上的烟细细飘散\] \[嫌疑人，轻飘飘，刻意漫不经心\]："跟我有关系吗。" \[老刑警，不抬头，嘴角微动\]："有。因为我从没输过。"_

[请至钉钉文档查看附件《例子.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02moflex97vlzhqnc0uze&utm_medium=im_card&utm_scene=person_space&utm_source=im)

> _T2V Prompt：幽深的海底洞穴中，蓝紫色的生物荧光在岩壁上流动，水草随暗流轻轻摇曳。章鱼丈夫小心翼翼地捧回一颗闪着珍珠光泽的稀有海螺，八条触手交叠着轻轻献给妻子，眼神里满是骄傲与讨好。妻子伸出触手慢慢摩挲海螺表面，眼睛骤然放光，皮肤颜色随兴奋情绪瞬间从深蓝变成炽热的橙红，嘴角贪婪地咧开。她脑海中浮现出那只收藏无数宝贝的寄居蟹，脑袋里尽是闪光的珍宝画面，眼神愈发幽深。她缓缓扭动身体靠近丈夫，触手轻轻缠上他的手臂，声音如水流般柔滑却暗藏算计："他收藏了那么多宝贝……不如都归我们。" 章鱼丈夫猛地缩回触手，八只眼睛瞬间睁大，皮肤颜色急剧变成惊慌的灰白，身体不自觉地向后漂移，颤声低语："他是我的朋友。" 妻子触手一收，皮肤重新变回冷静的深蓝，眼神如深海般平静又危险："带他来。" 镜头在两张面孔之间极速切换，荧光光影在脸上流动，贪婪与惊惶在深海的沉默中剧烈碰撞。画面色彩诡谲瑰丽，戏剧张力窒息，动画寓言电影质感。_

## 2.4 中近景叙事能力突出

[请至钉钉文档查看附件《HappyHorse-20260425-0001.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mofl66xmvo5urf821im&utm_medium=im_card&utm_scene=person_space&utm_source=im)

> _T2V Prompt：__清晨的山林小路上，镜头缓慢推进，一双鞋踩在略微潮湿的泥土和落叶上，发出轻微而清脆的“沙沙”声。周围只有微风吹过树叶的“簌簌”声，偶尔传来几声清脆的鸟鸣，远处还能听到溪水流动的细小水声。整段画面强调山林环境的安静、湿润和自然回响，环境音真实细腻。_

[请至钉钉文档查看附件《HappyHorse-20260425-0001 (13).mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mofljkpj752wznevawd&utm_medium=im_card&utm_scene=person_space&utm_source=im)

> _T2V Prompt：请给我生成一段邵氏风格喜剧电影，欧美男士说中文，中国男人说英文。_

## 2.5 灵活、多样的创作体验

[请至钉钉文档查看附件《f3904636.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mogttiupn6ej6qbrak&utm_medium=im_card&utm_scene=person_space&utm_source=im)

[请至钉钉文档查看附件《model-gen-video\_bench\_035b950106350dc765f9490ee888ad2e.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mogttmextanr32furj&utm_medium=im_card&utm_scene=person_space&utm_source=im)

> V2V Prompt：_将视频中的环境背景从沙漠替换为壮阔的蔚蓝色大海，海面上有轻微的波浪，远方是热带岛屿的轮廓。天空是明亮的晴天，阳光洒在沙滩上。探险家保持原有的徒步姿势和装备，脚下是洁白的细沙。光影色调调整为清新的海滨风格，光线明亮，画面充满度假感与自由的气息，高清晰度，电影级画质。_

[请至钉钉文档查看附件《0260425\_4011\_0.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mogtnhiqcs2zuy81hge&utm_medium=im_card&utm_scene=person_space&utm_source=im)

[请至钉钉文档查看附件《HappyHorse-20260427-0001.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mogtnkv288k0699vr0s&utm_medium=im_card&utm_scene=person_space&utm_source=im)

> V2V Prompt：将视频中的背景从绿幕替换为高端时尚T台现场。背景是模糊的观众席和闪烁的聚光灯，地面是反光的黑色T台地板。光照效果明亮且具有专业摄影感，在模特的头发和肩膀边缘有精致的轮廓光（Rim light）。营造出时尚秀场的专业氛围，镜头呈现浅景深效果

# 优势场景

HappyHorse 1.0 在影视短剧制作、电商广告（含数字人口播）、社媒创意视频三大核心场景中表现优异。影视短剧场景中，其在剧情细节、光影氛围营造、角色一致性维持上能力较强；电商广告场景中，数字人口播自然真实、指令遵循度高，可支撑商家批量化素材生产；在社媒创意场景，能快速生成画面精良、节奏紧凑、具有高传播力的内容，适配多风格社媒形式，且图生视频优势显著，有效降低制作门槛。

## 3.1 影视短剧制作

短剧制作是AI视频生成最高频的场景之一。模型在仿真人剧的情感表演细节、光影氛围营造、角色一致性维持等方面均展现出较强能力，在海外真人剧场景中的面部质感也表现优秀。

典型能力：

*   情感表演细节丰富
    
*   光影效果可跨场景稳定复现
    
*   画面质量稳定，场景与服装一致性表现良好
    
*   人物面部质感真实，适用于海内外真人剧制作
    

[请至钉钉文档查看附件《bench\_7a002df2daae71b459c2c23d0e746f7a.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mocy21wc584l6jb3fpe&utm_medium=im_card&utm_scene=person_space&utm_source=im)

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/mxPOG5zoAxgwMnKa/img/87e155c7-d7cf-46f6-9dc6-6c44f9efad77.png)

> _I2V Prompt：A boy and the rusty robot stand under the cool glow of the full moon, gently holding hands with a deep bond; a tight close-up captures the boy looking sincere and kind, his lips moving softly to whisper, "we are friends"; the robot's luminous eyes flicker and pulse as it processes the message, responding in a stuttering, mechanical electronic voice, "we... are, we... are friends"; hearing this, the boy's expression lights up with pure joy, and he reaches out his hand to kindly stroke and pat the robot's weathered metal head; the camera pulls back to a wide shot._

[请至钉钉文档查看附件《HappyHorse-20260425-0001 (2).mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mofj6mhznlizt89uk9&utm_medium=im_card&utm_scene=person_space&utm_source=im)

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgXbPv8PamlWN/img/a9181a02-770e-49e8-82f3-bfe1cf07f06a.png)

> _I2V Prompt：Cinematic western standoff. A sun-bleached desert outpost with wind whistling through cracked, weather-beaten wooden slats. Two cowboys stand in a tense, physical confrontation, facing each other with hands hovering tensely over their holsters. In the far distance, dust devils dance across the shimmering, heat-distorted horizon. Extreme close-ups capture the sweat on their brows, the grit of their skin, and the subtle, rhythmic trembling of their fingers near the gun belts. The dialogue plays out in the tension: The older cowboy spits on the ground, 'You kept your word.' The younger one replies sharply, 'I kept my promise.' The older man narrows his eyes, 'The price is too high.' The younger one looks him straight in the eye, 'It’s my price to pay.' The older man exhales, 'Then draw.' The younger one whispers, 'As you wish.' The aesthetic is gritty and Leone-inspired, featuring sharp high-contrast visuals, a palette of sepia and burnt orange, deep dramatic shadows, 35mm film grain, and a heavy, thick atmosphere of impending violence._

## 3.2 电商广告（包括数字人口播）

HappyHorse 1.0 在电商内容生产场景中已得到充分验证，覆盖产品广告、商品展示、口播带货等核心链路。模型生成的视频画面质感高、产品还原度好，数字人口播自然流畅，能够有效支撑商家从素材制作到投放的规模化内容生产需求。

典型能力：

*   产品展示视频清晰度高、质感优，图生视频对商品细节的还原度表现领先
    
*   数字人口播形象自然，五官协调、面部轮廓真实，告别"假人感"
    
*   指令遵循度高，画面构图、人物动作等均能精准响应 prompt 设定，降低反复调试成本
    
*   支持基于已有商品图快速生成视频素材，适配电商大促、日常上新等高频、批量化的素材生产需求
    

[请至钉钉文档查看附件《lQbPKG56xh421MkAALBJ7YEcV8Dn9QnEKanXcUkA.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mofv1wfp8539ough6p&utm_medium=im_card&utm_scene=person_space&utm_source=im)

> _T2V Prompt：一个年轻的漂亮女企业家优雅的坐在椅子上接受采访。采访场景辅助背景，虚化的办公环境/书架/绿植，轻微景深变化营造空间感，光线柔和均匀不抢主体，镜头几乎静止仅有微呼吸感，专业访谈节目质感，生成口播视频，主播说：其实我们从一开始就很明确，核心目标是解决用户真正在意的问题，而不是单纯追求技术上的突破。_

[请至钉钉文档查看附件《HappyHorse-20260427-0001.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mogv4hcsj1a9lqu79cn&utm_medium=im_card&utm_scene=person_space&utm_source=im)

> _T2V Prompt：高清电商直播间，年轻气质女性主播，妆容干净自然，温柔大方，简约网红穿搭，坐在轻奢直播台前，背景简约 ins 风货架、产品陈列灯牌，柔光补光灯、环形灯打光，画面明亮通透。主播面带微笑，手势自然讲解产品、展示细节、手拿商品对着镜头推荐，口播带货动作流畅，近距离上半身镜头，轻微缓慢运镜，画面流畅丝滑，写实真人质感，4K 超清，高饱和度，抖音快手短视频风格，沉浸式带货氛围。_

## 3.3 社媒创意视频

HappyHorse 1.0在社媒创意场景中表现出色，擅长生成具有高传播力的视觉内容。无论是产品种草、品牌故事、热点借势还是达人混剪，模型均能快速产出画面精良、节奏紧凑的短视频素材，帮助创作者降低制作门槛、提升内容吸引力与分发效率。

典型能力：

*   画面质感高，生成内容"第一眼抓人"，天然适配社媒平台的信息流场景
    
*   运镜与转场流畅，支持快节奏剪辑风格，提升完播率
    
*   多风格适配，可覆盖种草、测评、品牌宣传、剧情短片等多类社媒内容形式
    
*   图生视频还原度高，博主/品牌方可基于已有图片素材快速生成视频，实现"图文转视频"的高效内容扩展
    

![IMG_2268.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgXbPv8PamlWN/img/fab75735-2e23-4edc-bfe3-ee31e0b71003.jpeg)

[请至钉钉文档查看附件《HappyHorse-20260425-0016.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mofik7ktzzgg8g2bq2&utm_medium=im_card&utm_scene=person_space&utm_source=im)

> _I2V Prompt：菠萝摆了几个可爱的pose，然后用河南话说：老乡，你吃饭了没，要不要吃美味的大菠萝。_

[请至钉钉文档查看附件《0138\_seed60159\_\_\_Core\_Summary\_Two\_r.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02moczk29x4j1nvad0eax&utm_medium=im_card&utm_scene=person_space&utm_source=im)

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/mxPOG5zoAxgwMnKa/img/f84b7d94-85f6-41dd-9932-59c75f9eebc4.png)

> _I2V Prompt：直播间里，两只猫咪以拟人化形象做搞笑对话，要求写实，使用台湾中年男腔调。银色猫先说话：台词“他说他要当网红”。【1-5秒】画面：银色猫扭头面向金色猫，身子站立，伸着一只前爪，尾巴摇动，动作自然。金色猫说话：台词“靠什么火？”。【5-10秒】画面：金色猫扭头看向银色猫后身子站立，伸着一只爪子，满脸不屑的表情，动作自然。银色猫说话：台词“拍我们”金色猫说话：台词“那火的是我们，关他什么事”银色猫说话：台词“他说他负责帅”金色猫说话：台词“帅在哪？”要求语速适中，不要抢话，最后2只猫一起哈哈哈哈哈大笑起来，笑声洪亮，动作表情跟对话内容要严丝合缝。_

[请至钉钉文档查看附件《0092\_seed12466\_\_\_Core\_Summary\_This\_.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mocvwonj6gu93eqx39&utm_medium=im_card&utm_scene=person_space&utm_source=im)

![92.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/mxPOG5zoAxgwMnKa/img/7d6cc889-86cc-469c-b5d0-049015f4e261.jpeg)

> _I2V Prompt：这是一段具有电影级质感的AI生成视频，采用4K超高清画质。画面呈现出一种严肃的中国古代武侠大片氛围，却通过角色形象与道具的极度反差营造出强烈的冷幽默感。_

> _开场： 中景镜头，水獭皇帝威严地询问：“is this your handbag”（这是你的手提包吗？），随后镜头快速切换到橘猫。_

> _互动： 采用经典的对白切镜。特写镜头捕捉橘猫惊愕、瞪圆双眼的丰富表情。橘猫先是充满疑惑地低声说：“pardon”（请再说一遍？）。_

> _结尾： 橘猫在确认手包后，表情瞬间转为惊喜和乖巧，微笑着点头回应：“yes it is thank you very much”（是的，非常感谢），并伸手准备接包。_

# 提示词技巧

## 4.1 提示词公式

:::
提示词（prompt）是指正向提示词，用来描述视频中所包含的画面内容和运动过程，描述越准确、越丰富，生成视频的质量越高。

**提示词 = 场景+主体 + 运动 +音频**

**场景：**场景是主体所处的环境，包含背景、前景，可以是物理存在的真实空间或想象出来的虚构场景。

**主体：**主体是视频内容的主要表现对象，可以是人、动物、植物、物品或非物理真实存在的想象物体。

**运动：**运动包含主体的具体运动和非主体的运动状态，可以是静止、小幅度运动、大幅度运动、局部运动或整体动势
:::

[请至钉钉文档查看附件《0098\_seed50012\_\_\_Core\_Summary\_\_Insi (1).mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mocxpvo5h40kielapsg&utm_medium=im_card&utm_scene=person_space&utm_source=im)

> _T2V Prompt：_

> _【场景】奢华的私人飞机机舱内，窗外是壮丽的金红色的云海落日，阳光将机舱渲染成琥珀色。_

> _【主体】左侧满头银发的 \[ 年长男性 \] 身穿高定西装，手持威士忌酒杯，目光如鹰般锐利；右侧的 \[ 年轻男性 \] 身体微微前倾，眉头微皱，神情既紧张又充满野心。_

> _【运动】年长男性轻轻晃动着手中的酒杯，液体挂壁，他身体逼近对方；年轻男性深吸一口气，眼神坚定地回视。镜头缓慢侧推，聚焦两人之间紧绷的张力。_

> _【音频】\[ 年长男性, 低沉沙哑, 充满威严 \] 说道：“In this world, you either hunt or you become the prey. Which one are you?”  \[ 年轻男性, 嗓音紧绷但坚定 \] 回答：“I am the one who pulls the trigger.” 背景伴随着飞机引擎深沉的轰鸣声和冰块撞击玻璃杯的清脆声。_

## 4.2 首帧图生视频

以一张图片作为视频的起始画面（首帧），模型基于该图片内容生成后续的动态视频。上传的图片即为视频第一帧，确保画面起点与你的预期完全一致。

适用场景：

*   有一张满意的设计稿或插画，想让它"动起来"
    
*   需要精确控制视频的开场画面
    
*   基于产品图、人像照等现有素材快速生成动态展示
    

:::
提示词参考示例：

画面中的女孩缓缓转头微笑，微风吹动发丝，镜头保持不动，电影质感，自然光

咖啡杯中升起袅袅热气，镜头从俯拍缓慢拉远，暖色调，浅景深
:::

书写建议： 提示词中重点描述"动起来之后发生什么"——动作、运动轨迹、镜头变化等。无需重复描述图片中已有的静态内容，模型会自动识别首帧画面信息。

[请至钉钉文档查看附件《bench\_5f57b29f096f899aab5e01ffa578fb56 (1).mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02modxp7yjh85xdd8jsnb&utm_medium=im_card&utm_scene=person_space&utm_source=im)

![a7cf6706-6dcc-4b81-9c97-924345f3ac08.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgXbPv8PamlWN/img/29ef7b28-bf50-4baf-8327-b6d8ef47847e.jpeg)

> _I2V Prompt：穿着背心的猴子疯狂地敲击键盘，随后他突然停下，露出无奈的神情，用爪子用力挠了挠头，叹气说道：“这年头，别说天王老子，就算是猴子来了都得工作！”；紧接着，镜头切近为猴子面部特写，猴子单手托着腮帮子陷入沉思，流露出悔恨的表情，说道：“早知道这边待遇这么差，之前就不从天庭辞职了，唉！我的猴肠都悔青咯！”猴子说完继续敲击键盘开始工作，镜头拉远。_

## 4.3 多图参考生视频

HappyHorse 1.0 支持通过多张图片引导视频生成，包括主体多视角参考、场景图参考、分镜图参考等多种用法。

上传图片时，如对图片顺序有要求，请按顺序上传。在提示词中可通过@「图片1」「图片2」……「图片n」进行准确指代。

适用场景：

*   需要保持角色在不同镜头中外观一致，提供同一角色的多角度照片作为参考
    
*   有明确的场景设定或美术风格板，希望视频还原特定的视觉风格
    
*   按照分镜脚本制作视频，将各分镜图依次上传引导生成
    
*   需要将多个元素（如角色 + 场景 + Logo）组合到同一段视频中
    

:::
提示词参考示例：

参考「图片1」中的角色形象，她走进「图片2」中的场景，推开门后回头微笑，镜头跟随，电影质感

提取「图片1」和「图片2」中的猫咪特征，生成它在窗台上打盹后被惊醒的画面，保持毛色和花纹一致

结合「图片1」的正面照和「图片2」的侧面照，生成该角色转身回眸的动态画面，保持五官和发型一致

以「图片1」为画面风格参考，「图片2」中的人物在樱花树下漫步，最后出现「图片3」中的 Logo，整体色调统一
:::

[请至钉钉文档查看附件《单击播放 \_ 双击全屏 (5).mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02mofstt5opvwwqmphryl&utm_medium=im_card&utm_scene=person_space&utm_source=im)

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgXbNRG8RjlWN/img/b7bcb425-f07f-43c6-a161-cb7b7565ba52.png)![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgXbNRG8RjlWN/img/af6b1f7d-d521-4064-b89d-3b11fd96a3dc.png)![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgXbNRG8RjlWN/img/a8b94ac4-6c80-4892-9082-ad3ce24d206c.png)![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgXbNRG8RjlWN/img/8698c4fc-5ff0-4a3f-a6c0-fa5354714a37.png)

> _R2V Prompt：生成一段皮克斯视频：镜头围绕办公桌前的女孩环绕运镜，女孩正坐在电脑前若有所思【图1】，过程中切镜，特写女孩的脸部特写【图2】，女孩的表情体现出百思不得其解的状态，而突然女孩眼前一亮，脸上立刻舒展浮现出惊喜的笑意【图3】，体现出女孩想到了一个好主意，而此时镜头继续环绕运镜，女孩思考得到答案后，开心的把脚翘到办公桌上并双手抱在脑后【图4】，体现出她非常愉悦放松的状态和心情。_

## 4.4 上传视频 + Prompt 编辑

对已有视频进行 AI 智能编辑，无需从零生成，在原片基础上实现精准修改。你可以通过文字提示词描述修改意图，也可以同时上传参考图片提供视觉引导，两种方式可灵活搭配使用。

适用场景：

*   对视频整体风格不满意，想转换画面氛围（如写实转动漫、白天转黄昏）
    
*   需要修改画面中的局部元素（如替换背景、改变服装颜色、添加天气特效）
    
*   有一张目标风格的参考图，希望视频整体视觉效果向其靠拢
    
*   需要将视频中的某个元素替换为参考图中的特定对象
    
*   对 AI 生成的视频做二次修正，微调动作或画面细节
    

:::
提示词参考示例：

将视频中的背景从现代城市替换为古风街道，青石板路，远处有飞檐亭台，保持人物动作不变

将整体画面风格转为吉卜力动画风格，色彩明亮柔和，保持原始运动轨迹

为画面添加飘落的雪花效果，地面逐渐覆盖薄雪，整体色调偏冷

参考「图片1」的画面风格，将视频整体色调和质感调整为与参考图一致，保持原始动作和构图

将视频中人物的服装替换为「图片1」中的服装样式，保持人物动作和面部不变
:::

书写建议： 提示词中明确指出"改什么"和"保留什么"。描述越具体，模型越能精准执行编辑，避免误改不需要调整的部分。

[请至钉钉文档查看附件《mixkit-times-square-during-a-sunny-day-4442-hd-ready (1).mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02moec7p4g39un5dsufja&utm_medium=im_card&utm_scene=person_space&utm_source=im)

[请至钉钉文档查看附件《model-gen-video\_bench\_29abfed7129d0a2fd0960262a3b4a0b0.mp4》。](https://alidocs.dingtalk.com/i/nodes/14lgGw3P8vxjwogPCp6oqM91V5daZ90D?cid=66001624294&corpId=dingd8e1123006514592&doc_type=wiki_doc&iframeQuery=anchorId%3DX02moec8los9g0egl0i3s8&utm_medium=im_card&utm_scene=person_space&utm_source=im)

> _V2V Prompt：_将城市变成赛博朋克风格

# HappyHorse平台操作指南

## 5.1 功能选择

| **我想...** | **模式** |
| --- | --- |
| 只有想法 | 视频生成：不传图，仅输入文字 |
| 一张图，想让它按想法动起来 | 视频生成：首帧模式 |
| 几张图，想组合它们的元素创作新视频 | 视频生成：参考模式 |
| 一段视频，想改它 | 视频编辑 |

## 5.2 文生视频

| **文生视频操作界面** |  |
| --- | --- |
| ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/mxPOG5za7JjrKnKa/img/67da6a4a-51bc-4090-9206-a5da44d24d48.png) |  |
| **输入规格** | *   ++**自然语言**++：必须填写，最多5000英文字符或2500汉字 |
| **输出规格** | *   **分辨率**：可选720P/1080P<br>    <br>*   **画幅**：可选16:9 / 9:16 / 3:4 / 4:3 /1:1<br>    <br>*   **时长**：3-15秒<br>    <br>*   **声音输出**：自带音效/语音 |
| **建议** | 1.  **描述要具体：**避免抽象描述（如"好看的风景"），应包含主体、动作、场景、镜头运动等细节（如"一只金毛犬在雪地中奔跑，镜头从低角度跟随拍摄"）<br>    <br>2.  **结构化描述：**建议按「主体 → 动作 → 场景/背景 → 镜头运动 → 风格/氛围」的顺序组织提示词<br>    <br>3.  **避免冲突指令：**不要同时描述矛盾的内容（如"静止的人在快速奔跑"），也不要在一段描述中堆叠过多主体和动作<br>    <br>4.  **时长与内容匹配：**简单动作（转头、挥手）用短时长（3-5s）；复杂剧情或镜头运动选较长时长（8-15s）<br>    <br>5.  **善用声音输出：**如果画面涉及说话、自然环境声（风声、水声），开启音效/语音生成可显著提升沉浸感 |

## 5.3 首帧生视频

| **首帧生视频操作界面** |  |
| --- | --- |
| ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/mxPOG5za7JjrKnKa/img/1e127893-2790-45f2-9cb5-c3777b2fea6c.png) |  |
| **输入规格** | *   ++**1张首帧图**++：<br>    <br>    *   **格式**：.jpg / .jpeg / .png/ .webp<br>        <br>    *   **大小**：不超过30MB<br>        <br>    *   **分辨率**：短边不小于300像素<br>        <br>    *   **画幅**：长宽比0.4 ~ 2.5<br>        <br>*   ++**自然语言**++：最多5000英文字符或2500汉字；可以不填写 |
| **输出规格** | *   **分辨率**：可选720P/1080P<br>    <br>*   **画幅**：与首帧图片一致<br>    <br>*   **时长**：3-15秒<br>    <br>*   **声音输出**：自带音效/语音 |
| **建议** | 1.  **首帧图质量至关重要：**短边建议 400 像素以上，720P 及以上清晰度最佳，避免模糊、压缩严重、有明显噪点的图片<br>    <br>2.  **主体应清晰完整：**首帧图中主体不要被遮挡或截断，保持完整的人物/物体姿态，模型才能合理推断后续运动<br>    <br>3.  **避免静态死板的构图：**选择带有动势暗示的图片（如起跑姿势、挥动手臂的瞬间）比完全静止的正面照效果更好<br>    <br>4.  **文字描述作为运动引导：**虽然提示词可以不填，但建议填写期望的动作和镜头运动（如"人物缓缓转身，镜头推近"），能显著提升可控性 |

## 5.4 参考图生视频

| **参考图生视频操作界面** |  |
| --- | --- |
| ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/mxPOG5za7JjrKnKa/img/8b827475-3180-4ee5-93f5-9dc0d6627e8c.png) |  |
| **输入规格** | *   ++**1-9张参考图**++<br>    <br>    *   **格式**: .jpg / .jpeg / .png/ .webp<br>        <br>    *   **大小**：不超过30MB<br>        <br>    *   **分辨率**：短边不小于300像素<br>        <br>    *   **画幅**：长宽比0.4 ~ 2.5<br>        <br>*   ++**自然语言（文本）**++：必须填写，最多5000英文字符或2500汉字 |
| **输出规格** | *   **分辨率**：可选720P/1080P<br>    <br>*   **画幅**：可选16:9 / 9:16 / 3:4 / 4:3 /1:1<br>    <br>*   **时长**：3-15秒<br>    <br>*   **声音输出**：自带音效/语音 |
| **建议** | 1.  **图片不宜过小**：短边400像素以上<br>    <br>2.  **图片越清晰越好**：720P以上，避免极小图、糊图、压缩严重的图<br>    <br>3.  多张参考图的**比例尽量一致**，且和目标视频比例接近为佳<br>    <br>4.  **参考图内容**：<br>    <br>5.  主体清晰完整，无遮挡，避免多主体混乱、文字水印过多、极端裁切<br>    <br>6.  多张参考图最好是同一主体<br>    <br>7.  **参考图顺序**：建议按期望的画面/剧情顺序传入参考图 |

## 5.5 视频编辑

| **视频编辑操作界面** |  |
| --- | --- |
| ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/mxPOG5za7JjrKnKa/img/71d1591e-34ee-4511-9a31-8fc1d1737b73.png) |  |
| **输入规格** | *   ++**1个视频**++：<br>    <br>    *   **格式**：.mp4 / .mov，H264编码<br>        <br>    *   **大小**：大小不超过100MB<br>        <br>    *   **分辨率：**短边不小于320像素；长边不大于2160像素<br>        <br>    *   **画幅**：长宽比0.4 ~ 2.5<br>        <br>*   ++**1-4张参考图片**++：<br>    <br>    *   **格式**：.jpg / .jpeg / .png/ .webp<br>        <br>    *   **大小**：不超过30MB<br>        <br>    *   **分辨率**：短边不小于300像素<br>        <br>    *   **画幅**：长宽比0.4 ~ 2.5<br>        <br>*   ++**自然语言**++：最多5000英文字符或2500汉字 |
| **输出规格** | *   **分辨率**：可选720P/1080P<br>    <br>*   **画幅**：与输入的视频保持一致<br>    <br>*   **时长**：3-15秒<br>    <br>*   **声音输出**：可选“保持原始视频声音”或“AI生成音效及语音” |
| **建议** | 1.  **输入视频质量：**尽量使用 720P 及以上分辨率、H264 编码的原始视频，避免多次压缩或转码后的素材<br>    <br>2.  **输入视频时长贴近目标时长：**输入视频时长建议与输出时长（3-15s）接近，过长的视频截取关键片段后再上传，否则会自动截断。<br>    <br>3.  **参考图与视频内容关联：**参考图应与视频中需要编辑/替换的元素相关（如替换人物穿搭、改变场景风格），无关的参考图会干扰生成效果<br>    <br>4.  **参考图数量适度：**编辑意图明确时 1-2 张参考图即可；仅在需要多角度/多元素替换时使用 3-4 张<br>    <br>5.  **提示词聚焦编辑意图：**描述应侧重于"需要改变什么"而非重复描述视频原有内容（如"将背景替换为雪景，保持人物动作不变"）<br>    <br>6.  **声音策略选择：**如果编辑后画面风格变化大（如从都市变为森林），建议prompt描述“生成音效相关的指令”；如果仅微调画面，选择无需对音频做任何描述例如“不要改变音频”这类指令就无需再描述。 |

# 附：更多详细应用指南

## 6.1 视频生成 ：从零做出一段视频

### 文生视频模式

没有现成视频素材时，用文字作为起点，直接生成视频。

**适用场景：**

*   脑中有画面构思，但没有任何图片或视频素材
    
*   需要快速验证创意方向，先出一版粗剪看效果
    
*   制作纯虚构/幻想场景（如外星球、梦境），没有现实素材可参考
    

**使用要点：**

*   提示词是唯一的输入，描述质量直接决定生成效果
    
*   建议按 「主体 + 动作 + 场景 + 镜头 + 风格」 的结构组织语言
    
*   简单动作用短时长（3-5s），复杂剧情选长（5-10s）、超长（10-15s）时长
    

### 首帧生视频模式

上传一张图片作为视频的第一帧画面，平台基于这张图"让画面动起来"。适合已有画面构思或照片、设计稿等素材，希望延展为动态内容的场景。

**适用场景：**

*   已有一张满意的照片/AI生成图/设计稿，想让它变成视频
    
*   对视频开头画面有精确要求（构图、人物姿态、色调等不能偏差）
    
*   电商产品图、海报主视觉等需要从静态升级为动态展示
    

**使用要点：**

*   首帧图的质量决定上限——清晰度越高、主体越完整，效果越好
    
*   提示词虽然可以不填，但强烈建议填写期望的动作和镜头运动（如"人物缓缓转身，镜头推近"），否则模型会自行猜测运动方式
    
*   输出画幅和分辨率与首帧图一致，请提前将图片裁剪为目标比例，避免主体被自动裁切
    

**关键限制：** 只能上传 1 张图片，且该图片锁定为视频的第一帧。

### 参考图生视频模式

上传 1-9 张参考图片，配合文字描述，生成视频。模型会从参考图中提取主体外观、风格、场景等信息，融合到生成的视频中。

**和首帧模式的核心区别：**首帧模式是"从这张图开始播"，参考图模式是"参考这些图来拍"。

|  | **首帧图生视频** | **参考图生视频** |
| --- | --- | --- |
| **图片作用** | 图片 = 视频第一帧画面，精确还原 | 图片 = 视觉参考素材，提取特征后融入视频 |
| **图片数量** | 仅 1 张 | 1-9 张 |
| **画面还原度** | 极高，第一帧几乎与原图一致 | 中等，模型参考但不逐像素还原 |
| **画幅/分辨率** | 跟随原图 | 可自由选择（16:9 / 9:16 等） |
| **提示词** | 可不填（但建议填） | **必须填写** |
| **典型用途** | "让这张图动起来" | "基于这些素材，创作一段新视频" |

**多图组合 Prompt 的常见写法**

**写法一：单主体 + 多角度/多状态**

上传同一角色/产品的多角度照片，让模型更完整地理解主体外观。

> 上传素材：角色正面照、侧面照、全身照共3张

> 提示词：一位短发女性穿着红色大衣走在雨中的东京街头，撑着透明雨伞，霓虹灯倒映在湿润的地面上，镜头从正面缓慢移到侧面跟拍，电影感画面。

**写法二：主体 + 场景分离**

一部分图提供角色/产品外观，另一部分图提供目标场景或背景。

> 上传素材：图1-2为产品图（一款运动鞋），图3为场景参考（沙漠日落）

> 提示词：一双白色运动鞋从沙丘顶部滚落，沙粒飞溅，背景是金色日落，镜头跟随鞋子运动轨迹，慢动作，广告质感。

**写法三：多主体交互**

上传不同角色/物体的参考图，在提示词中描述它们之间的互动。

> 上传素材：图1为一只橘猫，图2为一只黑色拉布拉多

> 提示词：一只橘猫和一只黑色拉布拉多在草地上追逐嬉戏，橘猫跳到拉布拉多背上，阳光明媚，绿色草坪，中景拍摄，自然抓拍风格。

**写法四：剧情分镜/故事线**

按画面顺序上传参考图，模型会尝试按图片顺序组织视频内容。

> 上传素材：图1为咖啡豆特写，图2为手冲咖啡过程，图3为一杯拉花咖啡成品

> 提示词：展示手冲咖啡的完整过程，从咖啡豆研磨开始，到热水缓缓注入滤杯，最后呈现一杯精美的拿铁拉花，暖色调，微距与中景交替，ASMR氛围感。

**多图使用的注意事项**

*   多张图的比例尽量一致，且与目标视频比例接近
    
*   多张图最好围绕同一主题，避免塞入无关图片干扰模型理解
    
*   图片顺序有意义——按期望的画面/剧情顺序排列参考图
    
*   提示词必须填写，且应明确描述每组图的用途和期望的画面内容，不要让模型自己猜
    

## 6.2 视频编辑：修改已有视频

 已有视频（平台生成的或自己的），希望局部修改而不是重新生成整段。

### 场景一 ：风格化改写

画面内容、构图、人物动作都不变，只换视觉风格。

**适合场景：**

*   实拍视频变成动漫/油画/水彩/像素风
    
*   普通影像转成赛博朋克、蒸汽波、复古胶片等风格
    
*   给日常素材加上电影级调色和质感
    

**素材准备：**

*   原视频：画面主体清晰、构图稳定的素材效果最好；晃动严重或主体模糊的视频改写后容易崩
    

**Prompt 写法：**

*   描述目标风格的视觉特征，不重复描述原视频里的人物和场景
    
*   风格词要具体：不写"文艺风"，写"日系胶片质感，柔和逆光，淡雅色调"
    
*   可以指定色调、笔触、年代、媒介
    

**提示词示例：**

> 转成吉卜力动画风格，手绘质感，饱和度提高，天空更蓝，保持人物动作和镜头不变。

> 换成赛博朋克风格，霓虹光效，雨夜街道的反光，冷色调为主，人物轮廓保持清晰。

**注意：**

*   风格化幅度越大，人物面部细节可能会变化。
    
*   某些极端风格（如纯线稿、纯剪影）会丢失原视频的动作细节，慎用。
    

### 场景二 ：主体替换

画面动作、场景、镜头运动不变，换掉画面里的人、物、服装、发型等。

**适合场景：**

*   换装：同一段走路视频试不同穿搭
    
*   换发型/换造型：测试不同视觉形象
    
*   换手中道具：咖啡杯变酒杯、书变手机
    
*   换产品：一段展示视频换成不同商品
    

**素材准备：**

*   原视频：被替换的主体在画面里要清晰可见、动作连贯
    
*   参考图：参考图中包含想替换的形象
    
    *   换装 → 服装平铺图或穿着图
        
    *   换道具 → 道具清晰正面图
        
    *   换发型 → 发型参考图，最好构图角度和原视频接近
        

**提示词要点：**

*   明确指出**替换什么**和**保留什么**
    
*   用“图1”精确指向参考图
    
*   反向强调"其他不变"能降低模型在其他地方乱改的概率
    

**示例 prompt：**

> 把女孩的红色T恤换成图1的白色亚麻衬衫，牛仔裤换成图2的米色阔腿裤，场景、动作、光线、镜头都保持不变。

> 把桌上的马克杯换成图1的玻璃红酒杯，其他所有元素保持不变。

### 场景三 ：场景迁移

人物和动作不变，把背景/环境整体换掉。

**适合场景：**

*   室内变户外、城市变自然
    
*   白天变黑夜、晴天变雨天
    
*   现实场景变奇幻场景（日常街道 → 漂浮岛屿 / 外星地表）
    
*   季节迁移（夏 → 冬，春 → 秋）
    

**素材准备：**

*   原视频：主体和背景有明显区分的视频更容易做，比如人在纯色墙前、产品在简洁桌面上。
    
*   参考图：参考图是目标场景。
    

**Prompt 写法：**

*   强调"背景/场景替换"，同时**明确保留主体**
    
*   描述目标场景的光线、氛围、时间
    
*   如果新场景光线和原视频差异大（比如室内转户外正午），prompt 里可以补充"让主体光线匹配新场景"，否则人物可能看起来"贴"在场景上
    

**示例 prompt：**

> 将背景换成雪山场景，人物动作和姿态保持不变，调整人物身上的光线匹配雪地反光。

> 把场景从室内咖啡馆换成海边黄昏，保留人物和桌上的咖啡杯，让画面带上金色夕阳光。

**注意：**

*   涉及人物和场景交互的视频（比如手扶着栏杆）场景迁移风险高，新场景里可能没有对应的交互对象，选素材时应注意
    

### 场景四：多元素组合改写

一次编辑同时处理 2–3 个改动（比如换装 + 换场景）。

**适合场景：**

*   想在一次生成里完成多处改动，节省积分
    
*   改动之间有关联，分开改会造成风格不一致
    

**Prompt写法：**

*   用分句结构，每句对应一个改动，每个改动明确参考图片
    

**示例prompt：**

> 把女孩的衣服换成图1的白裙，场景换到图2的樱花林，光线换成图3这种柔和的午后逆光，动作、镜头、表情保持不变

**注意：**

*   3个以上并列改动的处理稳定性会下降，超过3个改动建议分两次完成
    

国际版：[《HappyHorse 1.0 Creative Guide》](https://alidocs.dingtalk.com/i/nodes/YQBnd5ExVEjea40qC2wDZERmJyeZqMmz?utm_scene=person_space)
