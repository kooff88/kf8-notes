# 目录

-[siege网站压力测试工具](#siege网站压力测试工具)


# siege网站压力测试工具

    1.下载最新版本 siege-4.0.2.tar.gz

    2.进入下载的文件夹目录位置
        输入命令 tar zxf siege-4.0.2.tar.gz
        $ cd siege-4.0.2/
        $ ./configure
        $ sudo make
        $ sudo make install
        
    3.查看siege安装路径:
      $ which siege
      /usr/local/bin/siege

      查看siege版本:
      $ siege -V
      SIEGE 4.0.2    
      
    4.（1）siege -c 20 -r 10 http://www.cnwytnet.com  进行测试
    参数说明： -c 是并发量，并发数为20人 -r 是重复次数， 重复10次

    (2) 随机选取urls.txt中列出所有的网址

      在当前目录下创建一个名为"urls-demo.txt"的文件。 文件里边填写URL地址，可以有多条，每行一条，比如：

      # URLs:
      http://www.sogou.com/web?query=php&from=wang_yong_tao
      https://www.baidu.com/
      // 执行 $ siege -c 5 -r 10 -f urls-demo.txt $ siege -c 5 -r 10 -f /Users/WangYoungTom/temp/urls-demo.txt

      参数说明： -c 是并发量，并发数为5人 -r 是重复次数， 重复10次 -f 指定使用文件，urls-demo.txt就是一个文本文件，每行都是一个url，会从里面随机访问的

      Siege从Siege-V2.06起支持POST和GET两种请求方式。 如果想模拟POST请求，可以在urls-demo.txt中安装一下格式填写URL:

      # URL （POST）:
      http://wangtest.com/index.php POST UserId=XXX&StartIndex=0&OS=Android&Sign=cff6wyt505wyt4c
      http://wangtest.com/articles.php POST UserId=XXX&StartIndex=0&OS=iOS&Sign=cff63w5905wyt4c
      使用示例:

      // 请求http://www.cnwytnet.com，并发人数为10，重复5次，每次请求间隔3秒
      $ siege --concurrent=10 --reps=5 --delay=3 http://www.cnwytnet.com
      $ siege -c 10 -r 5 -d 3 http://www.cnwytnet.com
      结果说明:

      Transactions: 153 hits (处理次数，本次处理了153此请求)
      Availability: 100.00 % (可用性/成功次数的百分比,比如本次100%成功)
      Elapsed time: 17.22 secs （运行时间，本次总消耗17.22秒）
      Data transferred: 7.70 MB （数据传送量）
      Response time: 0.17 secs （响应时间）
      Transaction rate: 8.89 trans/sec (处理请求频率，每秒钟处理8.89次请求）
      Throughput: 0.45 MB/sec （吞吐量,传输速度）
      Concurrency: 1.54 (实际最高并发连接数)
      Successful transactions: 153 (成功的传输次数)
      Failed transactions: 0 (失败的传输次数)
      Longest transaction: 0.70 (处理传输是所花的最长时间)
      Shortest transaction: 0.02 (处理传输是所花的最短时间)