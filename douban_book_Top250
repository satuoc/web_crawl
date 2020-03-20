import requests
import re
import time

# 通用代码框架
def getHTMLText(url):
    headers = {
     'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.88 Safari/537.36',
     'Cookies':'ll="118209"; bid=2L02TY_GX4U; __utma=30149280.1282056899.1583758170.1583758170.1583758170.1; __utmc=30149280; __utmz=30149280.1583758170.1.1.utmcsr=(direct)|utmccn=(direct)|utmcmd=(none); __utmt=1; gr_user_id=383b4b10-d648-4a2b-8353-5cdb486d7c79; gr_session_id_22c937bbd8ebd703f2d8e9445f7dfd03=154ebaad-12f8-4705-ba69-d1572b745b15; gr_cs1_154ebaad-12f8-4705-ba69-d1572b745b15=user_id%3A0; _pk_ref.100001.3ac3=%5B%22%22%2C%22%22%2C1583758175%2C%22https%3A%2F%2Fwww.douban.com%2F%22%5D; _pk_ses.100001.3ac3=*; __utmt_douban=1; __utma=81379588.1537473642.1583758175.1583758175.1583758175.1; __utmc=81379588; __utmz=81379588.1583758175.1.1.utmcsr=douban.com|utmccn=(referral)|utmcmd=referral|utmcct=/; ap_v=0,6.0; gr_session_id_22c937bbd8ebd703f2d8e9445f7dfd03_154ebaad-12f8-4705-ba69-d1572b745b15=true; __yadk_uid=898mB7N3eM8IZdTnbCJKVFfkk32WPUux; __gads=ID=71b11598bd23ee4c:T=1583758175:S=ALNI_MY2OXMKRlhAfugtK91BooTR8k5Peg; _vwo_uuid_v2=DFB7D42DF9F9C477BCC5863914EC1F866|1378d195c9fa3f9fd7dfa7441839493b; _pk_id.100001.3ac3=0a820c6a9af5536f.1583758175.1.1583758189.1583758175.; __utmb=30149280.4.10.1583758170; __utmb=81379588.3.10.1583758175'
    }
    try:
        r = requests.get(url, headers=headers, timeout=30)
        r.raise_for_status()  # 如果状态不是200，引发HTTPError异常
        r.encoding = r.apparent_encoding
        return r.text
    except:
        return "产生异常"

def parse_one_page(html):
    pattern = re.compile('<table.*?pl2.*?title="(.*?)".*?pl.*?>(.*?)</p>.*?rating_nums.*?>(.*?)</span>.*?</table>',
                         re.S)
    items = re.findall(pattern, html)
    for item in items:
        yield {
            'title':item[0].strip(),
            'author': item[1].split('/')[0].strip(),
            'score': item[2].strip()
        }

def main(start):
    url = 'https://book.douban.com/top250?start=' + str(start)
    html = getHTMLText(url)
    for item in parse_one_page(html):
        print(item)

if __name__ == '__main__':
    for i in range(10):
        main(start = i * 25)
        time.sleep(1)

