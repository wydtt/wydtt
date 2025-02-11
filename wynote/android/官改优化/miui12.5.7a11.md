卡刷包提取 
system.new.dat.br 
system.patch.dat 
system.transfer.list 

用dna-android软件分解br

不用点删除源文件他会自己删除

然后分解成一个system.img

然后继续分解这个img

分解成一个system文件夹 

普通的app data-app 和priv-app就不说了自己找合适的精简
app
anlaysiscore
hybridplatform                                                                                                 
然后就是里面预装了一些软件比如
uc浏览器 
优酷视频 
手机淘宝 
东方财富 
微博 
今日头条 
bilibili不vc                                                                                                                                        新
保留
知乎 支付宝 抖音

卡刷包中没有但是线刷包中有 所以没办法我们只好在刷入成功后在开机前执行

```c++
fastboot erase cust  
```
来擦除cust分区

然后手动卸载应用

搞好后我们将完成的system文件夹直接用
合成img-dat-br 所有都默认需要要改2处
打包类型选择br不是img,注意
然后我们将这个放到原卡刷包中即可刷入 

刷入之前
