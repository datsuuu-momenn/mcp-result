
首先让我们查看 `layout_model.py`：

Ran tool
从代码中我可以看到Layout Model使用的是ds4sd/docling-models模型，下载URL是：https://huggingface.co/ds4sd/docling-models

让我们继续查看 `table_structure_model.py`：

Ran tool
让我来总结一下各个OCR引擎和模型的下载URL:

1. Layout Model和Table Structure Model:
- 都使用 Hugging Face 模型库: https://huggingface.co/ds4sd/docling-models
- 版本: v2.2.0

2. EasyOCR:
让我查看 `easyocr_model.py`:

Ran tool
让我来总结一下 EasyOCR 的配置:

1. 模型文件位置:
- 默认路径: `settings.cache_dir/models/EasyOcr/`
- 可以通过 `model_storage_directory` 参数自定义

2. 支持的语言模型:
- 检测模型: "craft" 
- 识别模型: "english_g2", "latin_g2"

3. 硬件加速:
- 支持 CUDA 和 MPS 加速
- 通过 `accelerator_options.device` 配置

4. 其他重要参数:
- `confidence_threshold`: 置信度阈值
- `download_enabled`: 是否允许下载模型
- `scale`: 分辨率缩放倍数(默认为3,即72dpi -> 216dpi)

让我继续查看其他 OCR 引擎:

Ran tool
让我总结一下 RapidOCR 的配置:

1. 模型文件路径:
- 检测模型: `det_model_path`
- 分类模型: `cls_model_path`
- 识别模型: `rec_model_path`
- 字典文件: `rec_keys_path`

2. 硬件加速:
- 支持 CUDA 和 DirectML(DML)加速
- 通过 `accelerator_options.device` 配置
- 可设置线程数 `intra_op_num_threads`

3. OCR 参数:
- `text_score`: 文本置信度阈值
- `use_det`: 是否使用检测
- `use_cls`: 是否使用分类
- `use_rec`: 是否使用识别
- `print_verbose`: 是否打印详细信息

4. 图像处理:
- 默认分辨率缩放为3倍(72dpi -> 216dpi)

让我继续查看 Tesseract OCR:

Ran tool
让我总结一下 Tesseract OCR 的配置:

1. 模型文件路径:
- 通过 `options.path` 设置 Tesseract 数据路径
- 需要设置 `TESSDATA_PREFIX` 环境变量指向语言模型目录

2. OCR 引擎配置:
- `PSM` (Page Segmentation Mode): 默认为 `AUTO`
- `OEM` (OCR Engine Mode): 默认为 `DEFAULT`
- 支持多语言识别,使用 `+` 连接多个语言代码
- 支持自动语言检测 (`lang="auto"`)

3. 图像处理:
- 默认分辨率缩放为3倍(72dpi -> 216dpi)
- 支持区域识别(SetRectangle)
- 支持方向检测(DetectOrientationScript)

4. 输出参数:
- 文本置信度(MeanTextConf)
- 支持 UTF-8 文本输出
- 返回文本行级别的边界框

5. 特殊功能:
- 支持脚本(script)检测
- 支持 OSD (Orientation and Script Detection)
- 可以获取组件图像(GetComponentImages)

让我们继续查看其他 OCR 引擎的配置。我将查看 OCR Mac 模型:

Ran tool
让我总结一下 Mac OCR 的配置:

1. 系统要求:
- 仅支持 macOS 系统
- 需要安装 `ocrmac` 包 (`pip install ocrmac`)

2. 模型配置:
- 通过 `OcrMacOptions` 类配置参数
- 支持硬件加速选项 (`AcceleratorOptions`)
- 默认分辨率缩放为 3 倍(72dpi -> 216dpi)

3. OCR 参数:
- `recognition`: 识别级别设置
- `framework`: OCR 框架选择
- `language_preference`: 语言偏好设置
- 支持置信度阈值过滤

4. 图像处理:
- 支持区域识别(cropbox)
- 自动跳过面积为 0 的区域
- 支持临时文件处理图像

5. 输出格式:
- 返回文本单元格(TextCell)包含:
  - 文本内容
  - 置信度
  - 边界框坐标(左上右下)
  - OCR 来源标记
  - 索引编号

让我们继续查看 EasyOCR 的配置:

Ran tool
让我总结一下 EasyOCR 的配置:

1. 基本配置:
- 通过 `EasyOcrOptions` 类配置参数
- 默认分辨率缩放为 3 倍(72dpi -> 216dpi)
- 需要安装 `easyocr` 包 (`pip install easyocr`)

2. 模型配置:
- 支持多语言识别 (`lang_list`)
- 可配置模型存储目录 (`model_storage_directory`)
- 支持下载预训练模型:
  - 检测模型(如 "craft")
  - 识别模型(如 "english_g2", "latin_g2")

3. 硬件加速:
- 支持 GPU 加速(CUDA 和 MPS)
- 通过 `AcceleratorOptions` 配置设备
- 自动检测最佳设备

4. OCR 参数:
- 置信度阈值过滤
- 可选择识别网络(`recog_network`)
- 支持区域识别(cropbox)

5. 输出格式:
- 返回文本单元格(TextCell)包含:
  - 文本内容
  - 置信度
  - 边界框坐标
  - OCR 来源标记
  - 索引编号

让我们继续查看 RapidOCR 的配置:

Ran tool
让我总结一下 RapidOCR 的配置:

1. 基本配置:
- 通过 `RapidOcrOptions` 类配置参数
- 默认分辨率缩放为 3 倍(72dpi -> 216dpi)
- 需要安装 `rapidocr_onnxruntime` 包

2. 模型配置:
- 支持自定义模型路径:
  - 检测模型(`det_model_path`)
  - 分类模型(`cls_model_path`)
  - 识别模型(`rec_model_path`)
  - 识别字典(`rec_keys_path`)

3. 硬件加速:
- 支持多种加速设备:
  - CUDA GPU 加速
  - DirectML 加速
  - CPU 多线程(`intra_op_num_threads`)
- 通过 `AcceleratorOptions` 配置

4. OCR 参数:
- 文本置信度阈值(`text_score`)
- 可选择使用的功能:
  - 文本检测(`use_det`)
  - 文本分类(`use_cls`)
  - 文本识别(`use_rec`)
- 支持区域识别(cropbox)

5. 输出格式:
- 返回文本单元格(TextCell)包含:
  - 文本内容
  - 原始文本
  - 置信度
  - 边界框坐标
  - OCR 来源标记
  - 索引编号

让我们继续查看 Tesseract OCR 的配置:

Ran tool
让我总结一下 Tesseract OCR 的配置:

1. 基本配置:
- 通过 `TesseractOcrOptions` 类配置参数
- 默认分辨率缩放为 3 倍(72dpi -> 216dpi)
- 需要安装 `tesserocr` 包
- 需要正确设置 `TESSDATA_PREFIX` 环境变量指向 Tesseract 语言模型目录

2. 模型配置:
- 支持多语言识别:
  - 通过 `lang` 参数配置语言
  - 支持自动语言检测(`lang="auto"`)
  - 支持脚本检测(如 `script/Latin`, `script/Han` 等)
- 可配置模型路径(`path`)
- 支持不同的 OCR 引擎模式(`oem`)

3. 识别参数:
- 页面分割模式(`psm`):
  - 默认使用 `PSM.AUTO` 自动分割
  - 支持 `PSM.OSD_ONLY` 用于脚本检测
- 识别级别:
  - 使用 `RIL.TEXTLINE` 进行文本行级别识别
- 支持区域识别(cropbox)

4. 输出处理:
- 返回文本单元格(TextCell)包含:
  - 文本内容
  - 原始文本
  - 置信度
  - 边界框坐标(支持 TOPLEFT 坐标系)
  - OCR 来源标记
  - 索引编号

5. 调试功能:
- 支持可视化 OCR 结果(`settings.debug.visualize_ocr`)
- 提供详细的日志输出
- 包含错误处理和警告信息

这三种 OCR 引擎的主要区别是:

1. 易用性:
- EasyOCR: 安装简单,使用方便
- RapidOCR: 依赖 ONNX Runtime,部署灵活
- Tesseract: 需要额外配置环境变量和语言包

2. 语言支持:
- EasyOCR: 支持 80+ 种语言
- RapidOCR: 主要支持中英文
- Tesseract: 支持 100+ 种语言和脚本

3. 性能特点:
- EasyOCR: GPU 加速效果好,但速度较慢
- RapidOCR: 基于 ONNX 优化,速度快
- Tesseract: CPU 性能优秀,但准确率相对较低

4. 硬件要求:
- EasyOCR: 支持 CUDA/MPS
- RapidOCR: 支持多种加速设备
- Tesseract: 主要依赖 CPU

5. 应用场景:
- EasyOCR: 适合多语言场景
- RapidOCR: 适合对性能要求高的场景
- Tesseract: 适合简单文档和离线场景
