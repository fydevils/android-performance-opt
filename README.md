# android-performance-opt



- ![avatar](https://ws3.sinaimg.cn/large/006tNc79ly1g1wh7gllmmj30ui0jcdoo.jpg)





#性能分析工具
##### 1.LeakCanary   22k star
https://github.com/square/leakcanary

- ![avatar](https://ws2.sinaimg.cn/large/006tNc79ly1g1wh6rfr7aj30e806lt9h.jpg)


内存泄漏检测机制是什么？
 KeyedWeakReference与ReferenceQueue联合使用，在弱引用关联的对象被回收后，会将引用添加到ReferenceQueue；清空后，可以根据是否继续含有该引用来判定是否被回收；判定回收， 手动GC, 再次判定回收，采用双重判定来确保当前引用是否被回收的状态正确性；如果两次都未回收，则确定为泄漏对象。


##### 2.BlockCannry  4.9k star
https://github.com/markzhai/AndroidPerformanceMonitor

- ![avatar](https://ws3.sinaimg.cn/large/006tNc79ly1g1wh8g6oufj30jr0jemyt.jpg)

``` java
@Override
public void println(String x) {
    if (!mStartedPrinting) {
        mStartTimeMillis = System.currentTimeMillis();
        mStartThreadTimeMillis = SystemClock.currentThreadTimeMillis();
        mStartedPrinting = true;
    } else {
        final long endTime = System.currentTimeMillis();
        mStartedPrinting = false;
        if (isBlock(endTime)) {
            notifyBlockEvent(endTime);
        }
    }
}

private boolean isBlock(long endTime) {
    return endTime - mStartTimeMillis > mBlockThresholdMillis;
}

```

##### 3.GT   3.6K star
https://github.com/Tencent/github

什么是GT？
GT（随身调）是APP的随身调试平台，它是直接运行在手机上的“集成调试环境”(IDTE, Integrated Debug Environment)。

利用GT，仅凭一部手机，无需连接电脑，即可对APP进行快速的性能测试(CPU、内存、流量、电量、帧率/流畅度等等)、开发日志的查看、Crash日志查看、网络数据包的抓取、APP内部参数的调试、真机代码耗时统计等。


<img style="width:30%;height:30%" src="https://ws3.sinaimg.cn/large/006tNc79ly1g1wh9vliz2j30u01rcwhg.jpg"  align=center />
<img style="width:30%;height:30%" src="https://ws3.sinaimg.cn/large/006tNc79ly1g1wh8ysrioj30u01rcmzs.jpg"  align=center />
<img style="width:30%;height:30%" src="https://ws3.sinaimg.cn/large/006tNc79ly1g1wha60dz4j30u01rcq4o.jpg"  align=center />
<img style="width:30%;height:30%" src="https://ws3.sinaimg.cn/large/006tNc79ly1g1whaey6t4j30u01rcgn6.jpg"  align=center />
<img style="width:30%;height:30%" src="https://ws2.sinaimg.cn/large/006tNc79ly1g1whatb8hsj30u01rcq4o.jpg"  align=center />
<img style="width:30%;height:30%" src="https://ws2.sinaimg.cn/large/006tNc79ly1g1whb9x4snj30u01rc78m.jpg"  align=center />
<img style="width:30%;height:30%" src="https://ws3.sinaimg.cn/large/006tNc79ly1g1whbhpm6ej30u01rc0v2.jpg"  align=center />
<img style="width:30%;height:30%" src="https://ws2.sinaimg.cn/large/006tNc79ly1g1whbu9z8fj30u01rcjtq.jpg"  align=center />
<img style="width:30%;height:30%" src="https://ws1.sinaimg.cn/large/006tNc79ly1g1whc3i169j30u01rcmyz.jpg"  align=center />
<img style="width:30%;height:30%" src="https://ws2.sinaimg.cn/large/006tNc79ly1g1whcencwej30u01rcn1v.jpg"  align=center />
<img style="width:30%;height:30%" src="https://ws1.sinaimg.cn/large/006tNc79ly1g1whcljvufj30u01rc76t.jpg"  align=center />
<img style="width:30%;height:30%" src="https://ws3.sinaimg.cn/large/006tNc79ly1g1whcqudcej30u01rctat.jpg"  align=center />


#### 这是测试下载图片等功能的 内嵌代码
``` java 
			/*
			 *  GT usage
			 * 与GT控制台连接，同时注册输入输出参数
			 */
            GT.connect(getApplicationContext(), new AbsGTParaLoader() {

                @Override
                public void loadInParas(InParaManager inPara) {
					/*
					 * 注册输入参数，将在GT控制台上按顺序显示
					 */
                    inPara.register(并发线程数, "TN", "1", "2", "3");
                    inPara.register(KeepAlive, "KA", "false", "true");
                    inPara.register(读超时, "超时", "5000", "10000","1000");
                    inPara.register(连接超时, "连超时", "5000", "10000","1000");

                    // 定义默认显示在GT悬浮窗的3个输入参数
                    inPara.defaultInParasInAC(并发线程数, KeepAlive, 读超时);

                    // 设置默认无效的一个入参（GT1.1支持）
                    inPara.defaultInParasInDisableArea(连接超时);
                }

                @Override
                public void loadOutParas(OutParaManager outPara) {
					/*
					 * 注册输出参数，将在GT控制台上按顺序显示
					 */
                    outPara.register(下载耗时, "耗时", false, "ms");
                    outPara.register(实际带宽, "带宽", false, "KB/s");
                    outPara.register(singlePicSpeed, "SSPD", false, "KB/s");
                    outPara.register(NumberOfDownloadedPics, "NDP");

                    // 定义默认显示在GT悬浮窗的3个输出参数
                    outPara.defaultOutParasInAC(下载耗时, 实际带宽, singlePicSpeed);
                }
            });
```

##### 4.Emmagee
https://www.jianshu.com/p/a539a167d7dc
##### 5.ITest
##### 6.TestIn



