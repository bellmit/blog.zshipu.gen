
---
title: Golang通过http.NewRequest实现模拟请求，添加请求头
author: 知识铺
date: 2021-09-22 16:42:05+08:00
tags: [go]
---

Golang通过http.NewRequest实现模拟请求，添加请求头和请求参数

1.  ```func DownloadString(remoteUrl string,queryValues url.Values) (body []byte,err error){```

2.  ```client := &http.Client{};```

3.  ```body = nil;```

4.  ```uri,err := url.Parse(remoteUrl);```

5.  ```if(err != nil){```

6.  ```return ;```

7.  ```}```

8.  ```if(queryValues != nil){```

9.  ```values := uri.Query();```

10.  ```if(values != nil){```

11.  ```for k,v := range values {```

12.  ```queryValues[k] = v;```

13.  ```}```

14.  ```}```

15.  ```uri.RawQuery = queryValues.Encode();```

16.  ```}```

17.  ```reqest, err := http.NewRequest("GET",uri.String(),nil);```

18.  ```reqest.Header.Add("Accept", "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8");```

19.  ```reqest.Header.Add("Accept-Encoding", "gzip, deflate");```

20.  ```reqest.Header.Add("Accept-Language", "zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3");```

21.  ```reqest.Header.Add("Connection", "keep-alive");```

22.  ```reqest.Header.Add("Host", uri.Host);```

23.  ```reqest.Header.Add("Referer", uri.String());```

24.  ```reqest.Header.Add("User-Agent", "Mozilla/5.0 (Windows NT 6.1; WOW64; rv:12.0) Gecko/20100101 Firefox/12.0");```

26.  ```response, err := client.Do(reqest)```

27.  ```defer response.Body.Close();```

28.  ```if(err != nil){```

29.  ```return ;```

30.  ```}```

32.  ```if response.StatusCode == 200 {```

33.  ```switch response.Header.Get("Content-Encoding") {```

34.  ```case "gzip":```

35.  ```reader, _ := gzip.NewReader(response.Body)```

36.  ```for {```

37.  ```buf := make([]byte, 1024)```

38.  ```n, err := reader.Read(buf)```

40.  ```if err != nil && err != io.EOF {```

41.  ```panic(err)```

42.  ```}```

44.  ```if n == 0 {```

45.  ```break```

46.  ```}```

47.  ```body = append(body,buf...);```

48.  ```}```

49.  ```default:```

50.  ```body, _ = ioutil.ReadAll(response.Body)```

52.  ```}```

53.  ```}```

54.  ```return ;```

55.  ```}```
