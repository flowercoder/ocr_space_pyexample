# ocr_space_pyexample
All ocr.space api using python

All code in main.py


def ocr_space_url(url, overlay=False, api_key='helloworld', language='eng', ocrengine=1):
    payload = {'url': url,
               'isOverlayRequired': overlay,
               'apikey': api_key,
               'language': language,
               'OCREngine': 5
               }
    r = requests.post('https://api.ocr.space/parse/image',
                      data=payload,
                      )
    data = json.loads(r.content.decode())
    return print(data)


def ocr_space_file(filename, overlay=False, api_key='helloworld', language='eng', ocrengine=1):
    payload = {'isOverlayRequired': overlay,
               'apikey': api_key,
               'language': language,
               'OCREngine': 5
               }
    with open(filename, 'rb') as f:
        r = requests.post('https://api.ocr.space/parse/image',
                          files={filename: f},
                          data=payload,
                          )
        data = json.loads(r.content.decode())
        return print(data)


def ocr_space_base64(base64, overlay=False, api_key='helloworld', language='eng', ocrengine=1):
    payload = {
        'isOverlayRequired': overlay,
        'apikey': api_key,
        'language': language,
        'base64image': base64,
        'OCREngine': ocrengine
    }
    r = requests.post('https://api.ocr.space/parse/image',
                      data=payload,
                      )
    data = json.loads(r.content.decode())
    return print(data)


# Link Image example:
url = 'https://i0.hdslb.com/bfs/archive/de22d11d787ac812f08c813bfc32b76f67852594.png'
test_url = ocr_space_url(url=url, language='eng')

# Upload Image example:

test_file = ocr_space_file(filename='yourfile', language='eng')

# Base64 Image example:
with open('yourfile', 'rb') as f:
    img = f.read()
    f = str(base64.b64encode(img), encoding='utf-8')
    data = f'data:image/png;base64,{f}'
    # print(data)
test_base64 = ocr_space_base64(base64=data, language='eng')
