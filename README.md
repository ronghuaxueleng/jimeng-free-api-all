
# Jimeng AI Free 服务

支持即梦超强图像生成能力，包含最新 **jimeng-4.5**、**jimeng-4.1** 文生图模型、文生图、图生图功能，视频生成模型（目前官方每日赠送 66 积分，可生成 66 次），零配置部署，多路 token 支持。

与 OpenAI 接口完全兼容。

## 更新日志

### 2024-12-08 v4.5 更新
- **修复 jimeng-4.5 模型**：修复模型映射名称错误（`high_aes_general_v45` → `high_aes_general_v40l`）
- **更新 API 协议**：同步最新即梦 API 协议，更新 `draft_content` 和 `metrics_extra` 结构
- **升级版本号**：`DRAFT_VERSION` 升级到 `3.3.4`
- **扩展分辨率支持**：支持 1k/2k/4k 多种分辨率和比例（1:1, 4:3, 3:4, 16:9, 9:16, 3:2, 2:3, 21:9）
- **默认分辨率提升**：默认分辨率从 1024x1024 提升到 2048x2048
- **新增字段支持**：添加 `intelligent_ratio`、`resolution_type`、`metadata` 等字段


## 免责声明

**逆向 API 是不稳定的，建议前往即梦 AI 官方 https://jimeng.jianying.com/ 体验功能，避免封禁的风险。**

**本组织和个人不接受任何资金捐助和交易，此项目是纯粹研究交流学习性质！**

**仅限自用，禁止对外提供服务或商用，避免对官方造成服务压力，否则风险自担！**

**仅限自用，禁止对外提供服务或商用，避免对官方造成服务压力，否则风险自担！**

**仅限自用，禁止对外提供服务或商用，避免对官方造成服务压力，否则风险自担！**

## 接入准备

从 [即梦](https://jimeng.jianying.com/) 获取 sessionid

进入即梦登录账号，然后 F12 打开开发者工具，从 Application > Cookies 中找到`sessionid`的值，这将作为 Authorization 的 Bearer Token 值：`Authorization: Bearer sessionid`

![example0](./doc/example-0.png)

### 多账号接入

你可以通过提供多个账号的 sessionid 并使用`,`拼接提供：

`Authorization: Bearer sessionid1,sessionid2,sessionid3`

每次请求服务会从中挑选一个。

## 效果展示

![image-20250910110743543](https://mypicture-1258720957.cos.ap-nanjing.myqcloud.com/Obsidian/image-20250910110743543.png)

![image-20250912225128406](https://mypicture-1258720957.cos.ap-nanjing.myqcloud.com/Obsidian/image-20250912225128406.png)

![img](https://mypicture-1258720957.cos.ap-nanjing.myqcloud.com/Obsidian/QQ_1757688779317.png)

多图合成

![img](https://mypicture-1258720957.cos.ap-nanjing.myqcloud.com/Obsidian/QQ_1757688787070.png)

文生视频3.0

![img](https://mypicture-1258720957.cos.ap-nanjing.myqcloud.com/Obsidian/QQ_1757688755495.png)



## Docker 部署

1.  **拉取代码库**
    ```bash
    git clone https://github.com/zhizinan1997/jimeng-free-api-all.git
    ```
    *   **提示**: 如果您已将此项目 Fork 到自己的 GitHub 账号，请将上述命令中的 `https://github.com/zhizinan1997/jimeng-free-api-all.git` 替换为**您自己 Fork 后的仓库地址**。

2.  **进入项目文件夹**
    ```bash
    cd jimeng-free-api-all
    ```

3.  **构建 Docker 镜像**
    ```bash
    docker build -t jimeng-free-api-all:latest .
    ```
    *   此命令将根据项目中的 `Dockerfile` 构建一个名为 `jimeng-free-api-all` 的本地镜像。

4.  **启动 Docker 容器**
    ```bash
    docker run -it -d --init --name jimeng-free-api-all -p 8000:8000 -e TZ=Asia/Shanghai jimeng-free-api-all:latest
    ```
    *   `-p 8001:8000`: 将宿主机的 `8001` 端口映射到容器内部的 `8000` 端口。您可以根据需要修改 `8001`。
    *   `-e TZ=Asia/Shanghai`: 设置容器内的时区为上海，确保日志和时间戳正确。

## dockerhub 镜像仓库
下载镜像
```bash
docker pull wwwzhouhui569/jimeng-free-api-all:latest
```
启动 Docker 容器
```bash
docker run -it -d --init --name jimeng-free-api-all -p 8001:8000 -e TZ=Asia/Shanghai wwwzhouhui569/jimeng-free-api-all:latest
```



## 接口列表

### 对话补全（绘制图像&生成视频）

目前支持与 openai 兼容的 `/v1/chat/completions` 接口，可自行使用与 openai 或其他兼容的客户端接入接口，模型名称包括：
- **文生图模型**：`jimeng-4.5`（推荐）、`jimeng-4.1`、`jimeng-4.0`、`jimeng-3.1`、`jimeng-3.0`、`jimeng-2.1`、`jimeng-2.0-pro`、`jimeng-2.0`、`jimeng-1.4`、`jimeng-xl-pro`
- **视频生成模型**：`jimeng-video-3.0`、`jimeng-video-3.0-pro`、`jimeng-video-2.0`、`jimeng-video-2.0-pro`

### 模型映射表

| 用户模型名 | 内部模型名 | 说明 |
|-----------|-----------|------|
| `jimeng-4.5` | `high_aes_general_v40l` | 最新模型，推荐使用 |
| `jimeng-4.1` | `high_aes_general_v41` | 高质量模型 |
| `jimeng-4.0` | `high_aes_general_v40` | 稳定版本 |
| `jimeng-3.1` | `high_aes_general_v30l_art_fangzhou` | 艺术风格 |
| `jimeng-3.0` | `high_aes_general_v30l` | 通用模型 |

### 支持的分辨率

**1k 分辨率：**
- 1:1 (1024x1024), 4:3 (768x1024), 3:4 (1024x768), 16:9 (1024x576), 9:16 (576x1024), 3:2 (1024x682), 2:3 (682x1024), 21:9 (1195x512)

**2k 分辨率（默认）：**
- 1:1 (2048x2048), 4:3 (2304x1728), 3:4 (1728x2304), 16:9 (2560x1440), 9:16 (1440x2560), 3:2 (2496x1664), 2:3 (1664x2496), 21:9 (3024x1296)

**4k 分辨率：**
- 1:1 (4096x4096), 4:3 (4608x3456), 3:4 (3456x4608), 16:9 (5120x2880), 9:16 (2880x5120), 3:2 (4992x3328), 2:3 (3328x4992), 21:9 (6048x2592)

使用文生图模型时支持智能多图生成（jimeng-4.5、jimeng-4.1、jimeng-4.0 支持连续场景、绘本故事等多张图片生成），使用视频模型时为视频生成。

### 视频生成

视频生成接口，支持通过直接调用video接口或通过chat接口使用视频模型生成视频。

**POST /v1/videos/generations**

header 需要设置 Authorization 头部：

```
Authorization: Bearer [sessionid]
```

请求数据：

```json
{
  "model": "jimeng-video-3.0",
  "prompt": "视频描述文本",
  "width": 1024,
  "height": 1024,
  "resolution": "720p",
  "filePaths": ["首帧图片路径", "尾帧图片路径"]
}
```

响应数据：

```json
{
  "videoUrl": "https://v9-artist.vlabvod.com/..."
}
```
其他模型可另选jimeng-video-3.0/jimeng-video-3.0-pro-jimeng-video-2.0/jimeng-video-2.0-pro


### 图像生成

图像生成接口，与 openai 的 [images-create-api](https://platform.openai.com/docs/api-reference/images/create) 兼容。

#### 文生图接口

**POST /v1/images/generations**

header 需要设置 Authorization 头部：

```
Authorization: Bearer [sessionid]
```

请求数据：

```json
{
  // 支持模型：jimeng-4.5（推荐）/ jimeng-4.1 / jimeng-4.0 / jimeng-3.1 / jimeng-3.0 / jimeng-2.1 / jimeng-2.0-pro / jimeng-2.0 / jimeng-1.4 / jimeng-xl-pro
  "model": "jimeng-4.5",
  // 提示词，必填。jimeng-4.5、jimeng-4.1、jimeng-4.0 支持多图生成，如"生成4张连续场景的图片"
  "prompt": "美丽的风景画，夕阳下的湖泊",
  // 反向提示词，默认空字符串
  "negative_prompt": "",
  // 图像宽度，默认2048（支持1k/2k/4k多种分辨率）
  "width": 2048,
  // 图像高度，默认2048
  "height": 2048,
  // 精细度，取值范围0-1，默认0.5
  "sample_strength": 0.5,
  // 响应格式：url 或 b64_json，默认 url
  "response_format": "url"
}
```

#### 图生图接口

**POST /v1/images/compositions**

支持多张输入图片的图像合成功能：

```json
{
  "model": "jimeng-4.5",
  "prompt": "将这些图片合成为一幅美丽的风景画",
  // 输入图片数组，支持 URL 字符串或对象格式
  "images": [
    "https://example.com/image1.jpg",
    {"url": "https://example.com/image2.jpg"},
    "https://example.com/image3.jpg"
  ],
  "negative_prompt": "",
  "width": 2560,
  "height": 1440,
  "sample_strength": 0.5,
  "response_format": "url"
}
```

响应数据：

```json
{
  "created": 1733593745,
  "data": [
    {
      "url": "https://p9-heycan-hgt-sign.byteimg.com/tos-cn-i-3jr8j4ixpe/61bceb3afeb54c1c80ffdd598ac2f72d~tplv-3jr8j4ixpe-aigc_resize:0:0.jpeg?lk3s=43402efa&x-expires=1735344000&x-signature=DUY6jlx4zAXRYJeATyjZ3O6F1Pw%3D&format=.jpeg"
    }
  ],
  "input_images": 3,
  "composition_type": "multi_image_synthesis"
}
```

#### 客户端 curl 调用示例

**文生图接口调用：**

```bash
curl -X POST http://localhost:8000/v1/images/generations \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your_sessionid_here" \
  -d '{
    "model": "jimeng-4.5",
    "prompt": "美丽的日落风景，湖边的小屋",
    "width": 2048,
    "height": 2048,
    "sample_strength": 0.7,
    "response_format": "url"
  }'
```

**jimeng-4.5 多图生成：**

```bash
curl -X POST http://localhost:8000/v1/images/generations \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your_sessionid_here" \
  -d '{
    "model": "jimeng-4.5",
    "prompt": "生成4张连续场景的图片：春夏秋冬四季风景",
    "width": 2048,
    "height": 2048,
    "sample_strength": 0.5
  }'
```

**图生图接口调用：**

```bash
curl -X POST http://localhost:8000/v1/images/compositions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your_sessionid_here" \
  -d '{
    "model": "jimeng-4.5",
    "prompt": "将这些图片合成为一幅充满创意的艺术作品",
    "images": [
      "https://example.com/image1.jpg",
      "https://example.com/image2.jpg"
    ],
    "width": 2560,
    "height": 1440,
    "sample_strength": 0.6,
    "response_format": "url"
  }'
```

**视频生成接口调用：**

```bash
curl -X POST http://localhost:8000/v1/videos/generations \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer your_sessionid_here" \
  -d '{
    "model": "jimeng-video-3.0",
    "prompt": "一只可爱的小猫在草地上玩耍",
    "width": 1024,
    "height": 1024,
    "resolution": "720p"
  }'
```


## 感谢

感谢 [jimeng-free-api-all](https://github.com/zhizinan1997/jimeng-free-api-all) 项目的贡献

感谢 [jimeng-free-api](https://github.com/LLM-Red-Team/jimeng-free-api) 项目的贡献
