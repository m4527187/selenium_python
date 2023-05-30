import time
from  selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.select import Select


#youtubede pytube+selenium+python kelimeleri aratıldı. izlanme sayısı, ne zaman yüklendi, konusu ve kimin tarafından
driver=webdriver.Firefox()
driver.maximize_window()
driver.get("https://www.youtube.com/results?search_query=selenium+python")
time.sleep(3)
last_height = driver.execute_script("return document.documentElement.scrollHeight")
print(last_height)
while True:
   mp=driver.page_source
   driver.execute_script("window.scrollTo(0, arguments[0]);", last_height)
   time.sleep(3)
   new_height = driver.execute_script("return document.documentElement.scrollHeight")
   print("bouyt=",mp.__sizeof__(),new_height)
   if new_height == last_height:
       break
   last_height = new_height
time.sleep(10)
r1=driver.find_elements(By.XPATH,"//*[@id='video-title']/yt-formatted-string")
d1=[]
d2=[]
d3=[]
for r1a in r1:
    v1=r1a.get_attribute("aria-label")
    v2=r1a.text
    v3=1+len(v2)
    v4=v1[v3:]
    d1.append(v1)
    d2.append(v2)
    d3.append(v4)
    print("-1-",v1)
    print("-2-", v2)
    print("-3-", v4)
    b = v4.find(" tarafından ")
    b1=v4[:(b+11)]
    print("-4-",b1)
    c = v4[(b + 12):]
    q1 = c.rfind("saniye")
    q2 = c.rfind("dakika")
    q3 = c.rfind("saat")
    m1 = q2
    m2 = 7
    if (q1 > q2):
        m1 = q1
        m2 = 7
    if (q3 > m1):
        m1 = q3
        m2 = 5
    f = c[(m1 + m2):]
    f = f.replace(" görüntüleme", "")
    f = f.replace(" görüntüleme - kısa videoyu oynat", "")
    f = f.replace(" - kısa videoyu oynat", "")
    f = f.replace(" Görüntüleme yok", "0")
    f = f.replace("Görüntüleme yok","0")
    print("-5-", f)
    g = c.find(f)
    h = c[:(g - 1)]
    print("-6-", h)

time.sleep(3)
driver.quit()
