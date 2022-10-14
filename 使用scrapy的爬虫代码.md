```python
import scrapy
import json
from JDMspider.items import JDcommentItem



class JMSpider(scrapy.Spider):
    name = 'JM'
    allowed_domains = ['www.jd.com']
    def start_requests(self):
        for m in range(0,500):
            yield scrapy.Request(url=f'https://club.jd.com/comment/productPageComments.action?&productId=100019125569&score=0&sortType=5&page={m}&pageSize=10',callback=self.parse)

    def parse(self, response):
        site = json.loads(response.text)
        site_small = site['comments']
        for i in range(len(site_small)):
            item = JDcommentItem()
            item['ID'] = site_small[i]['nickname']
            item['comment'] = site_small[i]['content']
            yield item
```

```python
import scrapy

#将爬虫得到的数据组装成Item对象
class JDcommentItem(scrapy.Item):
    # define the fields for your item here like:
    # name = scrapy.Field()
    ID = scrapy.Field()
    comment = scrapy.Field()
```

**使用scrapy的爬虫代码**

