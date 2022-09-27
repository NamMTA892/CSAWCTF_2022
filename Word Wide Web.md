# Đề bài
![Imgur](https://i.imgur.com/05IkEoD.png)

Link:http://web.chal.csaw.io:5010

Mở đầu bài này chúng ta sẽ hiện ra dòng chữ:  
![Imgur](https://i.imgur.com/nNh57AM.png)

Và khi bấm vào link Stuff thì đề sẽ hiện ra 1 đống Yolo cho các bạn tha hồ bấm:  
![Imgur](https://i.imgur.com/CB32qqD.png)

Đầu tiên mình sẽ nói hướng bài này: Ctrl+U (vào source), tìm các đường link bắt đầu bằng nhãn "a" và có chữ "href"  
### Cách 1:  
Cứ như vậy chúng ta sẽ có Script:
```
from array import array  
import requests  
from bs4 import BeautifulSoup  

BASE_URL = 'http://web.chal.csaw.io:5010'  

r1 = requests.get(BASE_URL)  

soup = BeautifulSoup(r1.text, 'html.parser')  

array = []  
cookies = r1.cookies  

for link in soup.findAll('a'):  
    array.append(link.get('href'))  

while True:  
    r2 = requests.get(BASE_URL + array[0], cookies=cookies)  
    print(r2.text)  
    soup = BeautifulSoup(r2.text, 'html.parser')  
    href = ''  
    for link in soup.findAll('a'):  
        href = link.get('href')  
        if href != None:  
            print(href)  
            cookies = r2.cookies  
            array.insert(0, href)  
            print(r2.content.decode('utf-8'))  
            # print(array)  
            break  
```

hoặc
```
import requests  

url = "http://web.chal.csaw.io:5010/"  
session = requests.Session()  

with session :  
	next_word = 'stuff'  
	while  True:  
		response1 = session.get(url+next_word)  
		"""print(session.cookies)"""  
		try:  
			startingIndex=response1.text.index('href="/')  
			endText = response1.text[startingIndex:].index('">')  
		except :  
			print(response1.text)  
			break  
		print("next word:",response1.text[7+startingIndex:endText+startingIndex])  
		next_word = response1.text[7+startingIndex:endText+startingIndex]  
```
### Cách 2:  
Sử dụng wget để download file về:  
``` 
wget -m http://web.chal.csaw.io:5010  
```
Sau đó sử dụng lệnh grep:  
```
cat * | grep -i ctf
```
![Imgur](https://i.imgur.com/lCf2eAN.png)
