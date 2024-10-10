# python
import os
import re

import requests
url = "https://pic.netbian.com/uploads/allimg/241010/180750-1728554870129b.jpg"
headers = {
    "user-agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36 Edg/129.0.0.0"
}
response =  requests.get(url=url, headers=headers)
print(response.text)
response.encoding = response.apparent_encoding
parr = re.compile('src="(/u.*?)".alt="(.*?)“')
image = re.findall(parr, response.text)
path = "CS职业哥帅照"

if not os.path.exists(path):
    os.makedirs(path)

for i in image:
    link = i[0]
    name = i[1]
    with open(path+"/{}.jpg".format(name),"wb") as img:
        res = requests.get("https://pic.netbian.com/4kyouxi/.com"+link)
        img.write(res.content)
        img.close()
        print(name+".jpg 获取成功......")
