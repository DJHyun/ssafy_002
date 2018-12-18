# 2018년 12월 18일

## 로또

### 1~45 까지의 숫자를 가진 배열을 만든다.

python make long array / make number array

numbers에서 숫자 6개를 랜덤으로 뽑는다.(당연히 비복원 추출)

랜덤으로 뽑은 숫자들을 lotto 변수에 담고 출력한다.

추가 : lotto 변수에 담겨있는 숫자들을 오름차순으로 정렬하기

```python


import random



numbers = range(1,46)

lotto = random.sample(numbers,6)

lotto.sort()
print("이번주 로또 번호는 {0} 입니다.".format(lotto))


```



## 로또번호

```python
import requests
import random
from bs4 import BeautifulSoup

url = 'https://m.dhlottery.co.kr/common.do?method=main'
response = requests.get(url).text
soup = BeautifulSoup(response, 'html.parser')
document = soup.select('.prizeresult')[0]
numbers = document.select('span')
ns = []
for i in numbers:
  ns.append(int(i.text))

lotto = sorted(random.sample(list(range(1,46)),6))

print(ns)
print(lotto)

cnt = 0
'''
result = []
for i in ns:
  for j in lotto:
    if(i == j):
      cnt += 1
      result.append(i)
      break
'''
for i in ns:
  if i in lotto:
    cnt += 1
    
print("{}개 맞았습니다".format(cnt))
```









## 네이버웹툰

1. 네이버 웹툰을 가져올 수 있는 주소(url)를 파악하고 url 변수에 저장한다.
2. 해당 주소로 요청을 보내 정보를 가져온다.
3. 받은 정보를 bs를 이용해 검색하기 좋게 만든다.
4. 네이버 웹툰 페이지로 가서, 내가 원하는 정보가 어디에 있는지 파악한다.
  오늘자 업데이트 된 웹툰들의 각각 리스트 페이지, 웹툰의 제목 + 해당 웹툰의 썸네일
5. 3번에서 저장한 문서를 이용해 4번에서 파악한 위치를 뽑아내는 코드를 작성한다.
6. 출력한다.

```python
import requests
import time
from bs4 import BeautifulSoup as bs

today = time.strftime("%a").lower()



naver_url = 'https://comic.naver.com/webtoon/weekdayList.nhn?week='+today
response = requests.get(naver_url).text
soup = bs(response,'html.parser')
toons = []
li = soup.select('.img_list li')

for item in li:
  toon = {"title":item.select('dt a')[0].text,
          "url": item.select('dt a')[0]["href"],
          "img_url":item.select('.thumb img')[0]['src']
         }
  toons.append(toon)
print(toons)
```



# 다음웹툰

1. 내가 원하는 정보를 얻을 수 있는 주소를 url이라고 하는 변수에 담는다.

2. 해당 url에 요청을 보내 응답을 받아 저장한다.

3. 구글신에게 python으로 어떻게 json을 파싱(딕셔너리 형으로 변환)하는지 물어본다.

4. 파싱한다.(변환한다)

5. 내가 원하는 데이터를 꺼내서 조합한다.

```python
import requests
import time
import json
from bs4 import BeautifulSoup as bs

url = "http://webtoon.daum.net/data/pc/webtoon/list_serialized/thu"

response = requests.get(url).text

document = json.loads(response)

data = document["data"]
toons = []
for toon in data:
  print(toon["title"])
  print(toon["pcThumbnailImage"]["url"])
  print("http://webtoon.daum.net/webtoon/view/{}".format(toon["nickname"]))
```





  

