def load_data(data_net_file,data_flow_file):
    G=nx.Graph()#用Graph方法建立一个空的无向图G，用来存网络结构。
    F=nx.DiGraph()#用DiGraph方法建立一个空的有向图F，用来存地点间的流量（因为从A到B和从B到A的流量可能不一样，所以这里用有向图）

    netfile=open(data_net_file)#打开一个文件---网络数据。其实Python有专门的包处理csv文件读写
    flowfile=open(data_flow_file)#打开一个文件---流量数据。
    i=0    #设置一个计数器，为了避开读取csv文件的第一行标题

    for line in netfile: #循环读取文件netfile中的每一行数据，到文件末尾会自动结束。for in是Python最基本的循环语句，任何可遍历的对象都可以for in，例如for in数字范围range(n)，就是从0循环到n-1。

        if i>0:#从第二行开始读数据。if是条件控制语句，后面带条件表达式，然后用冒号与后面的语句分割（类似C里花括号的作用）。另外，凡是带冒号的语句（流程控制、函数定义等）后面的语句都要强制缩进，所以Python程序的可读性很好。

            col=line.split(',') #将文件中的一行按逗号分割，赋给一个数组col，然后用放括号加序号就可以引用数组中的元素了。当然，split也可以放其他字符作为分割符号。如果什么都不放，split()默认用空格和Tab分割字符串

            G.add_edge(col[0], col[1], dis=float(col[2])) #用add_edge方法为网络G添加一条含权的边，权重的名字是dis。注意距离是数字，因此需要用float将文本强制转换为浮点数

        i+=1
    netfile.close()#记得关掉用过的文件，Python会在后台释放内存。

    j=0 
    for fline in flowfile: 
        if j>0: 
             
            col=fline.split(',') 
            F.add_edge(col[0],col[1],flow=float(col[2])) 
            
        j+=1
    flowfile.close()#记得关掉用过的文件，Python会在后台释放内存。
    return G,F
   `````` 
if __name__=='__main__':
    net_file='net.csv'
    flow_file='flow.csv'
    G,F=load_data(net_file,flow_file)
    for u,v in G.edges():
        print u,v
    
``````
