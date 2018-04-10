import requests
import os
import re
import random

def url_open(url): #统一打开网页
    user_agent_list = [ \
            "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.1 (KHTML, like Gecko) Chrome/22.0.1207.1 Safari/537.1" \
            "Mozilla/5.0 (X11; CrOS i686 2268.111.0) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11", \
            "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.6 (KHTML, like Gecko) Chrome/20.0.1092.0 Safari/536.6", \
            "Mozilla/5.0 (Windows NT 6.2) AppleWebKit/536.6 (KHTML, like Gecko) Chrome/20.0.1090.0 Safari/536.6", \
            "Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.1 (KHTML, like Gecko) Chrome/19.77.34.5 Safari/537.1", \
            "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/536.5 (KHTML, like Gecko) Chrome/19.0.1084.9 Safari/536.5", \
            "Mozilla/5.0 (Windows NT 6.0) AppleWebKit/536.5 (KHTML, like Gecko) Chrome/19.0.1084.36 Safari/536.5", \
            "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1063.0 Safari/536.3", \
            "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1063.0 Safari/536.3", \
            "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_0) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1063.0 Safari/536.3", \
            "Mozilla/5.0 (Windows NT 6.2) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1062.0 Safari/536.3", \
            "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1062.0 Safari/536.3", \
            "Mozilla/5.0 (Windows NT 6.2) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1061.1 Safari/536.3", \
            "Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1061.1 Safari/536.3", \
            "Mozilla/5.0 (Windows NT 6.1) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1061.1 Safari/536.3", \
            "Mozilla/5.0 (Windows NT 6.2) AppleWebKit/536.3 (KHTML, like Gecko) Chrome/19.0.1061.0 Safari/536.3", \
            "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/535.24 (KHTML, like Gecko) Chrome/19.0.1055.1 Safari/535.24", \
            "Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/535.24 (KHTML, like Gecko) Chrome/19.0.1055.1 Safari/535.24"
        ]
    Referer = url
    ua = random.choice(user_agent_list)
    headers = {'User-Agent': ua,"Referer":Referer}
    html = requests.get(url,headers = headers).content
    return html

def get_page(url):

    req = url_open(url).decode('utf-8')
    re.findall(r'',req)


##   ----------------------find()出现较高重复次数，改用正则表达---------------        
##    a = req.find('http://www.mzitu.com/') + 21
##    b = req.find('"',a)

    addrs_l1 = re.findall(r'http://www.mzitu.com/\d\d\d\d\d\d',req) #存在重复数据
    addrs = list(set(addrs_l1))
    addrs.sort(key=addrs_l1.index) #删除重复并保持顺序不变
    print(addrs)

    return addrs
    


def find_imgs(url):
    req = url_open(url).decode('utf-8')
    img_addrs = []
    img_num = int(re.findall(r'<span>\d{1,2}</span>',req)[-1][6:8])
    for i in range(img_num):
        i += 1
        html = url + "/" + str(i )
        req = url_open(html).decode('utf-8')
        a = req.find('img src=')
        b = req.find('.jpg',a)
        img_addrs.append(req[a+9:b+4])
            


    for each in img_addrs:
        print(each)    
    return img_addrs
    
    
    
def save_imgs(folder,img_addrs):
##    ref = []
##    for each_line in img_addrs:
##        each = each_line + '\n'   #强行加换行符
##        ref.append(each )
##    file_name = file_num + '.txt'
##    content = open(file_name,'w')
##    content.writelines(ref)
##    content.close()
    for each in img_addrs:
        filename = each.split('/')[-1]
        print(filename)
        with open(filename,'wb') as f:
            img = url_open(each)
            f.write(img)
            
            
        


def download_mm(folder = 'file'):
    pages = int(input('请输入需要爬取的页数：\n'))
    

    File_Path = os.getcwd() + '\\' + folder       #获取到当前文件的目录，并检查是否有report文件夹，如果不存在则自动新建report文件
    if not os.path.exists(File_Path):
        os.mkdir(folder)
    
    os.chdir(folder)

    url = "http://www.mzitu.com/"

    page_url = get_page(url)
    
    for i in range(pages):       
        print(page_url[i])
##        file_num = str(page_url[i].split('/')[-1])#抓取地址序号
        
        img_addrs = find_imgs(page_url[i])
        
        save_imgs(folder,img_addrs)

if __name__ == '__main__':
    download_mm()
