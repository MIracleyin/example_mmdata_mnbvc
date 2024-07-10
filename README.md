## mnbvc mm dataset v2.0

MNBVC 多模态语料数据格式。原链接：https://huggingface.co/datasets/wanng/example_mmdata_mnbvc

|字段名称|字段说明|可选|
|-|-|-|
|实体ID|数据的唯一标识符。用于在数据集中确定是哪一条数据。在单个数据集中确定一条数据的实体对象。|必选|
|块ID|一个实体对象内的标识符。用于确定一条数据内的一个部分数据。parquet 行的最小单元。 |必选|
|时间|语料首次出现的时间，如无法确定则为处理该数据实体的时间 |必选|
|扩展字段|用于保存块的元信息。为可以被成功 load 的 json 字符串。后期可继续扩展 |必选|
|文本|文本块的内容 |必选 |
|图片|图片块的内容 |必选 |
|OCR文本|图片的 OCR 结果 |必选 |
|音频|音频块的内容 |必选 |
|STT文本|音频的 STT 结果 |必选 |
|块类型|用于保存块的类别。为字符串，使用该类型可以从内容中提取对应信息。类别的含义为“模态”。 |必选|
|文件md5|当 entity/blcok 是从对应文件解析时，需要计算文件 md5 用于标识数据完整性 |可选|
|页ID|当文件从文档中解析时，需要计算当前页数 |可选|

每一行文本/图片/音频只能存在一条内容，OCR文本、STT文本 暂时留空。

图片读取代码：

``` python

def read_image(image_path):
    # 打开图像文件
    with open(image_path, 'rb') as file:
        image = Image.open(file)
        # 将图像转换为二进制格式
        img_byte_arr = io.BytesIO()
        image.save(img_byte_arr, format=image.format)
        img_byte_arr = img_byte_arr.getvalue()
    return img_byte_arr
```

音频读取代码：
``` python
def read_audio(audio_path):
    # 使用PyDub读取音频文件
    audio = AudioSegment.from_wav(audio_path,)
    # 创建一个BytesIO对象
    byte_arr = io.BytesIO()
    # 将音频保存为二进制格式
    audio.export(byte_arr, format="wav")
    # 获取二进制数据
    audio_bytes = byte_arr.getvalue()

    return audio_bytes
```

 