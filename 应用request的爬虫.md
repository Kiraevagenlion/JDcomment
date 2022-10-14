```python
import requests
import json


def get(page_number):
    url='https://club.jd.com/comment/productPageComments.action?productId=100019125569&score=0&sortType=5'
    headers = {
        'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/104.0.5112.81 Safari/537.36 Edg/104.0.1293.54'}
    x = {
        "page": page_number,
        "pageSize": "10",
    }
    comment= requests.get(url=url, headers=headers, params=x)
    site = comment.text
    site_dit = json.loads(site)
    item = site_dit['comments']
    return item
if __name__ == "__main__":  
    for it in range(0,51):
        item = get(it)
        for dit in item:
            nickname = dit['nickname']
            content = dit['content']
            print(nickname, content,)
            fp = open("D:txt", "a", encoding='utf-8')
            fp.write(str(item))
            fp.write(nickname)
            fp.write(content)
            fp.close()
```

**运用request库做的爬虫**

*pass(部分在李鼎铭同学指导下完成)*