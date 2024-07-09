## mnbvc mm dataset v2.0

MNBVC 多模态语料数据格式。原链接：

|字段名称|字段说明|可选|
|-|-|-|
|实体ID| | |
|块ID| | |
|时间| | |
|扩展字段| | |
|文本| | |
|图片| | |
|OCR文本| | |
|音频| | |
|STT文本| | |
|块类型| | |
|文件md5| | |
|页ID| | |

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

 