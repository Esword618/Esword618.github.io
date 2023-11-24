# First_post


## 基于wsl搭建ROOT环境

[ROOT安装](https://ezcjzah48j.feishu.cn/docx/ZpCidtOyOoYfA0xJ53EcjnkqnZg) 

## root文件操作

### TTree文件格式

暂时无法在飞书文档外展示此内容

一个 Entrie 为一个 Event 存储信息

| Root 文件数据存储格式 | TTree |      | Branch-evtID | Branch-nPhotons | Branch-edep | ...  |
| :-------------------- | :---- | :--- | :----------- | :-------------- | :---------- | :--- |
| Entrie-0              | x1    | y1   | z1           | ...             |             |      |
| Entrie-1              | x2    | y2   | z2           | ...             |             |      |
| ...                   | x3    | y3   | z3           | ...             |             |      |

以`/junofs/users/luhq/juno/job/trunk190121/noOptical/rootdata/v0/data/M00.root`文件为例

```Python
rootFilePath = "../rootdata/M00.root"
f = TFile(rootFilePath)
f.ls()

------------------Output---------------------------
TFile**                ../rootdata/M00.root        
 TFile*                ../rootdata/M00.root        
  KEY: TTree        evt;1        evt
  KEY: TH1I        stepno;1        step number of optical photons
  KEY: TTree        geninfo;1        Generator Info
  KEY: TTree        TT;1        Deposit Energy TT
  KEY: TTree        TTDigit;1        PE TT
  KEY: TTree        opticalparam;1        Optical Parameters
  KEY: TTree        mu;1        muon events
  KEY: TTree        muIso;1        isotope and neutron from muon spallation.
  KEY: TTree        mufastn;1        muon induced fast neutron
evt_tree = f.Get("evt") # 获取 evt TTree
# 打印 TTree 结构
evt_tree.Print()

------------------Output---------------------------
******************************************************************************
*Tree    :evt       : evt                                                    *
*Entries :  2997000 : Total =       374747740 bytes  File  Size =   24274338 *
*        :          : Tree compression factor =  15.52                       *
******************************************************************************
*Br    0 :evtID     : evtID/I                                                *
*Entries :  2997000 : Total  Size=   12079214 bytes  File Size  =    4292703 *
*Baskets :      999 : Basket Size=      32000 bytes  Compression=   2.81     *
*............................................................................*
*Br    1 :nPhotons  : nPhotons/I                                             *
*Entries :  2997000 : Total  Size=   12082223 bytes  File Size  =     158841 *
*Baskets :      999 : Basket Size=      32000 bytes  Compression=  75.94     *
*............................................................................*
*Br    2 :totalPE   : totalPE/I                                              *
*Entries :  2997000 : Total  Size=   12081220 bytes  File Size  =     157842 *
*Baskets :      999 : Basket Size=      32000 bytes  Compression=  76.41     *
*............................................................................*
... 省略
# 输出 Branch 信息，从Entrie从0-9，感觉不实用
evt_tree.Scan("*", "", "", 10, 0)

------------------Output---------------------------
***********************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************
*    Row   * Instance * evtID.evt * nPhotons. * totalPE.t *   nPE.nPE * energy.en * hitTime.h * pmtID.pmt * PETrackID * edep.edep * edepX.ede * edepY.ede * edepZ.ede * isCerenko * isReemiss * isOrigina * OriginalO * nPMTs.nPM * nPE_byPMT * PMTID_byP * LocalPosX * LocalPosY * LocalPosZ * LocalDirX * LocalDirY * LocalDirZ * GlobalPos * GlobalPos * GlobalPos * BoundaryP * BoundaryP * BoundaryP *
***********************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************
*        0 *        0 *         0 *         0 *         0 *           *           *           *           *           *         0 *         0 *         0 *         0 *           *           *           *           *         0 *           *           *           *           *           *           *           *           *           *           *           *           *           *           *
*        1 *        0 *         1 *         0 *         0 *           *           *           *           *           *         0 *         0 *         0 *         0 *           *           *           *           *         0 *           *           *           *           *           *           *           *           *           *           *           *           *           *           *
*        2 *        0 *         2 *         0 *         0 *           *           *           *           *           * 2397.4184 * 14677.919 * 2181.8515 * 7268.2172 *           *           *           *           *         0 *           *           *           *           *           *           *           *           *           *           *           *           *           *           *
*        3 *        0 *         3 *         0 *         0 *           *           *           *           *           *         0 *         0 *         0 *         0 *           *           *           *           *         0 *           *           *           *           *           *           *           *           *           *           *           *           *           *           *
*        4 *        0 *         4 *         0 *         0 *           *           *           *           *           *         0 *         0 *         0 *         0 *           *           *           *           *         0 *           *           *           *           *           *           *           *           *           *           *           *           *           *           *
*        5 *        0 *         5 *         0 *         0 *           *           *           *           *           * 4616.1396 * 2092.5810 * -13239.65 * -3952.277 *           *           *           *           *         0 *           *           *           *           *           *           *           *           *           *           *           *           *           *           *
*        6 *        0 *         6 *         0 *         0 *           *           *           *           *           *         0 *         0 *         0 *         0 *           *           *           *           *         0 *           *           *           *           *           *           *           *           *           *           *           *           *           *           *
*        7 *        0 *         7 *         0 *         0 *           *           *           *           *           *         0 *         0 *         0 *         0 *           *           *           *           *         0 *           *           *           *           *           *           *           *           *           *           *           *           *           *           *
*        8 *        0 *         8 *         0 *         0 *           *           *           *           *           *         0 *         0 *         0 *         0 *           *           *           *           *         0 *           *           *           *           *           *           *           *           *           *           *           *           *           *           *
*        9 *        0 *         9 *         0 *         0 *           *           *           *           *           *         0 *         0 *         0 *         0 *           *           *           *           *         0 *           *           *           *           *           *           *           *           *           *           *           *           *           *           *
***********************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************
# 输出 Entrie 为 1 的数据
# 下面 Show 输出的数据比上面的 Branch 少是因为，有需要的Branch没有数据
evt_tree.Show(1)

------------------Output---------------------------
======> EVENT:2
 evtID           = 2
 nPhotons        = 0
 totalPE         = 0
 edep            = 2397.42
 edepX           = 14677.9
 edepY           = 2181.85
 edepZ           = 7268.22
 nPMTs           = 0
```

### pyroot

#### My first tree

[tree-stydy-py-1.html](https://esword618.github.io/ROOT-project/html/tree-stydy-py-1.html)

##### 注意1（ctypes的类型要使用`.value`）

ctypes的类型要使用`.value`

```Python
from ctypes import c_double, c_int
from ROOT import TFile, TTree,TCanvas
guan = TFile("guan.root", "recreate")
ming = TTree("ming", "This is my first tree")
i = c_int(1)
a = c_double(2.2)
b = c_double(0.0)

# "i" 为分支的名称，i为地址（c_int本身就是地址，C++ 是通过&i）,"i/I"为i的类型
ming.Branch("i", i, "i/I")
ming.Branch("a", a, "a/D")
ming.Branch("b", b, "b/D")

for j in range(100):
    i.value = j  # 通过.value属性更新 ctypes 变量的值 （注意）
    a.value = i.value * 0.1
    b.value = j * j
    ming.Fill()
    
ming.Write()
guan.ls()
TFile**                guan.root        
 TFile*                guan.root        
  OBJ: TTree        ming        This is my first tree : 0 at: 0x55986256e2d0
  KEY: TTree        ming;1        This is my first tree
ming.Print()
******************************************************************************
*Tree    :ming      : This is my first tree                                  *
*Entries :      100 : Total =            4039 bytes  File  Size =       1499 *
*        :          : Tree compression factor =   2.23                       *
******************************************************************************
*Br    0 :i         : i/I                                                    *
*Entries :      100 : Total  Size=        945 bytes  File Size  =        248 *
*Baskets :        1 : Basket Size=      32000 bytes  Compression=   1.89     *
*............................................................................*
*Br    1 :a         : a/D                                                    *
*Entries :      100 : Total  Size=       1353 bytes  File Size  =        329 *
*Baskets :        1 : Basket Size=      32000 bytes  Compression=   2.64     *
*............................................................................*
*Br    2 :b         : b/D                                                    *
*Entries :      100 : Total  Size=       1353 bytes  File Size  =        413 *
*Baskets :        1 : Basket Size=      32000 bytes  Compression=   2.10     *
*............................................................................*
# 没有索引时，默认是最后一个
ming.Show()
======> EVENT:-1
 i               = 99
 a               = 9.9
 b               = 9801
```

##### 注意2（Scan 函数在vscode的jupyter lab中使用有问题，在jupyter lab中是没有问题的（注意），这里仅仅打印20行。）

Scan 函数在vscode的jupyter lab中使用有问题，在jupyter lab中是没有问题的（注意），这里仅仅打印20行。

```Python
# Scan 函数在vscode的jupyter lab中使用有问题，jupyter lab在浏览器中打开是没有问题的（注意）
ming.Scan("*", "", "", 20, 0)
************************************************
*    Row   *       i.i *       a.a *       b.b *
************************************************
*        0 *         0 *         0 *         0 *
*        1 *         1 *       0.1 *         1 *
*        2 *         2 *       0.2 *         4 *
*        3 *         3 *       0.3 *         9 *
*        4 *         4 *       0.4 *        16 *
*        5 *         5 *       0.5 *        25 *
*        6 *         6 *       0.6 *        36 *
*        7 *         7 *       0.7 *        49 *
*        8 *         8 *       0.8 *        64 *
*        9 *         9 *       0.9 *        81 *
*       10 *        10 *         1 *       100 *
*       11 *        11 *       1.1 *       121 *
*       12 *        12 *       1.2 *       144 *
*       13 *        13 *       1.3 *       169 *
*       14 *        14 *       1.4 *       196 *
*       15 *        15 *       1.5 *       225 *
*       16 *        16 *       1.6 *       256 *
*       17 *        17 *       1.7 *       289 *
*       18 *        18 *       1.8 *       324 *
*       19 *        19 *       1.9 *       361 *
************************************************
%jsroot off
# jsroot可以交互式地浏览ROOT生成的图形
c1 = TCanvas("c1","test canvas",400,300);
ming.Draw("b:a","","colz");
c1.Draw()
```

![img](https://ezcjzah48j.feishu.cn/space/api/box/stream/download/asynccode/?code=ODdiN2IwNmIwZDIwYmUxMTA2NzFiNTEyNmI4NWYwOThfSkRpMFRobGh4dHFFSDhrbHBqYTJhdW5ySjBWNHVsaEZfVG9rZW46QkpremJMUWg4b3lzcml4MXlJdmNHeEp5bm1oXzE3MDA3ODg5MjI6MTcwMDc5MjUyMl9WNA)

```Python
c2 = TCanvas("c2","b:a",400,300)
ming.Draw("a:b","","colz")
c2.Draw()
```

![img](https://ezcjzah48j.feishu.cn/space/api/box/stream/download/asynccode/?code=NjkxYzE1Yjk2YzA1NmY3NGQzMDVjNjdlNDY2NjgxMDFfeHRhUzdjOWl2Um1DQ3dWeXJLT2VXNGkxcUh6WU5pdjhfVG9rZW46RDA2bmI1S1dVb2Y4U0t4QlNSa2NEVnN6bnljXzE3MDA3ODg5MjI6MTcwMDc5MjUyMl9WNA)

```Python
guan.Close()
```

#### My second tree

[tree-stydy-py-2.html](https://esword618.github.io/ROOT-project/html/tree-stydy-py-2.html)

```Python
from ctypes import c_double, c_int, c_float,c_ushort
from ROOT import TFile, TTree, TCanvas, TRandom
f = TFile("f-file.root","recreate")
t = TTree("t-tree","esword second tree")
r = TRandom()
px, py, pz = c_float(), c_float(), c_float()
random = c_double()
i = c_ushort()
t.Branch("px",px,"px/F")
t.Branch("py",py,"py/F")
t.Branch("pz",pz,"pz/F")
t.Branch("random",random,"random/D")
t.Branch("i",i,"i/s")
for ii in range(10000):
    r.Rannor(px,py)
    pz.value = px.value**2 + py.value**2
    random.value = r.Rndm()
    t.Fill()
f.Write()
t.Print()
******************************************************************************
*Tree    :t-tree    : esword second tree                                     *
*Entries :    10000 : Total =          223565 bytes  File  Size =     169026 *
*        :          : Tree compression factor =   1.31                       *
******************************************************************************
*Br    0 :px        : px/F                                                   *
*Entries :    10000 : Total  Size=      40627 bytes  File Size  =      37172 *
*Baskets :        2 : Basket Size=      32000 bytes  Compression=   1.08     *
*............................................................................*
*Br    1 :py        : py/F                                                   *
*Entries :    10000 : Total  Size=      40627 bytes  File Size  =      37178 *
*Baskets :        2 : Basket Size=      32000 bytes  Compression=   1.08     *
*............................................................................*
*Br    2 :pz        : pz/F                                                   *
*Entries :    10000 : Total  Size=      40627 bytes  File Size  =      36515 *
*Baskets :        2 : Basket Size=      32000 bytes  Compression=   1.10     *
*............................................................................*
*Br    3 :random    : random/D                                               *
*Entries :    10000 : Total  Size=      80738 bytes  File Size  =      57203 *
*Baskets :        3 : Basket Size=      32000 bytes  Compression=   1.40     *
*............................................................................*
*Br    4 :i         : i/s                                                    *
*Entries :    10000 : Total  Size=      20543 bytes  File Size  =        190 *
*Baskets :        1 : Basket Size=      32000 bytes  Compression= 105.63     *
*............................................................................*
t.Show(1) # Entries 为行数
======> EVENT:1
 px              = 1.57022
 py              = 0.579752
 pz              = 2.80171
 random          = 0.169346
 i               = 0
t.Scan("*", "", "", 20, 0)
************************************************************************
*    Row   *     px.px *     py.py *     pz.pz * random.ra *       i.i *
************************************************************************
*        0 * 0.8966467 * -1.712815 * 3.7377111 * 0.7905995 *         0 *
*        1 * 1.5702210 * 0.5797516 * 2.8017063 * 0.1693463 *         0 *
*        2 * 0.6975117 * 0.1442547 * 0.5073320 * 0.8619950 *         0 *
*        3 * 0.0616207 * -1.009907 * 1.0237097 * 0.8942667 *         0 *
*        4 * -0.054552 * 1.3832200 * 1.9162737 * 0.7776606 *         0 *
*        5 * -2.017178 * 1.4682819 * 6.2248592 * 0.3903101 *         0 *
*        6 * 0.8903368 * 2.5101616 * 7.0936112 * 0.8544955 *         0 *
*        7 * -1.098390 * -0.318103 * 1.3076509 *   0.33476 *         0 *
*        8 * 0.3865155 * 0.0235152 * 0.1499472 * 0.1494743 *         0 *
*        9 * 1.8970719 * 1.9546536 * 7.4195528 * 0.9352411 *         0 *
*       10 * 0.6802427 * 0.1985776 * 0.5021632 * 0.5868942 *         0 *
*       11 * 0.5670135 * 0.0129729 * 0.3216726 * 0.3481201 *         0 *
*       12 * -1.043177 * 0.6455513 * 1.5049554 * 0.6848344 *         0 *
*       13 * 0.1561114 * 1.7405016 * 3.0537166 * 0.4606435 *         0 *
*       14 * -0.408388 * 0.9339914 * 1.0391209 * 0.1496268 *         0 *
*       15 * -0.002963 * -0.304645 * 0.0928176 * 0.4394039 *         0 *
*       16 * -0.058236 * 1.2137416 * 1.4765603 * 0.9567470 *         0 *
*       17 * -0.777734 * 2.2816205 * 5.8106622 * 0.7270176 *         0 *
*       18 * 0.1255596 * -0.128900 * 0.0323806 * 0.0892672 *         0 *
*       19 * -0.834347 * -2.053497 * 4.9129881 * 0.2138195 *         0 *
************************************************************************
c3 = TCanvas("c3","px:py",400,300);
t.Draw("px:py","","colz")
c3.Draw()
```

![img](https://ezcjzah48j.feishu.cn/space/api/box/stream/download/asynccode/?code=YjQyOTJjNWUyNmEyY2ZmNjg4YzU0NGQ2ZjYwODEzOWNfdUhMNGw1MzkyM2N3bjhScDE2OTlRZlJKVEN5UGhYdnhfVG9rZW46R3JVZWIybVg1bzM0RDF4aHRvdGNWWUwybmljXzE3MDA3ODg5MjI6MTcwMDc5MjUyMl9WNA)

```Python
c4 = TCanvas("c4","px:pz",400,300);
t.Draw("px:pz","","colz")
c4.Draw()
```

![img](https://ezcjzah48j.feishu.cn/space/api/box/stream/download/asynccode/?code=MTUyYWU1YTEyNmQyMDc2YTg2OTQ2NDgyYWYzOGZjYjlfWUVCaDY3Z090UVk0c1Fmbktlb0c5cHQ1UDVWNEVxdTlfVG9rZW46TDFHdGJJSW9Mb1g5d3V4UWI3eWNCaUVRbmNoXzE3MDA3ODg5MjI6MTcwMDc5MjUyMl9WNA)

##### Tcut筛选

```Python
t.Show(4)
======> EVENT:4
 px              = -0.0545523
 py              = 1.38322
 pz              = 1.91627
 random          = 0.777661
 i               = 0
```

这里Tcut理解成条件画图筛选数据的条件，t.Draw("py","i==0","L") 中 i==0 就是条件。

```Python
c5 = TCanvas("c5","tcut",400,300)
# i==0就是一个选择条件（注意）
t.Draw("py","i==0","L")
c5.Draw()
```

![img](https://ezcjzah48j.feishu.cn/space/api/box/stream/download/asynccode/?code=OTQwYTViNTQ5OTU4NDJjMjYwM2JjMzU3YWY1N2VlMTdfZWNVZzBrWEtFcFREWUx5T0FrS1dockhLWWJJSm5yM0NfVG9rZW46QWJ6dGIxb1dRb2xnNWp4MkpuOGNsV0ZTbjVjXzE3MDA3ODg5MjI6MTcwMDc5MjUyMl9WNA)

```Python
f.Close()
```

##### vscode插件

[ROOT File Viewer](https://marketplace.visualstudio.com/items?itemName=albertopdrf.root-file-viewer)

该插件可以查看 root 文件

![img](https://ezcjzah48j.feishu.cn/space/api/box/stream/download/asynccode/?code=MDQwYzBhNGVjZjI1MzliNGJiNGE3MTBhZDM3YWJmYWVfcVdySTJTZnNMeE5uWmVHZ1VKeDNXOWdHNURjcGMzYUlfVG9rZW46R1NOT2I3dnQ2b2g5UUd4TDBnOWNjQW1GbndmXzE3MDA3ODg5MjI6MTcwMDc5MjUyMl9WNA)

### uproot

[github link](https://github.com/scikit-hep/uproot5)

[uproot 文档](https://uproot.readthedocs.io/en/latest/index.html)

```Python
import uproot
uproot.default_library # 设置全局使用 awkward 作为数据操作对象
rootFilePath = "../rootdata/M00.root"
file = uproot.open(rootFilePath)
file.classnames() ## flie.ls()

------------------Output---------------------------
{'evt;1': 'TTree',
 'stepno;1': 'TH1I',
 'geninfo;1': 'TTree',
 'TT;1': 'TTree',
 'TTDigit;1': 'TTree',
 'opticalparam;1': 'TTree',
 'mu;1': 'TTree',
 'muIso;1': 'TTree',
 'mufastn;1': 'TTree'}
file.keys()

------------------Output---------------------------
['evt;1',
 'stepno;1',
 'geninfo;1',
 'TT;1',
 'TTDigit;1',
 'opticalparam;1',
 'mu;1',
 'muIso;1',
 'mufastn;1']
file.values()

------------------Output---------------------------
[<TTree 'evt' (31 branches) at 0x7f8e9f70f2e0>,
 <TH1I (version 1) at 0x7f8e88483f40>,
 <TTree 'geninfo' (20 branches) at 0x7f8e88416ce0>,
 <TTree 'TT' (21 branches) at 0x7f8e88416d10>,
 <TTree 'TTDigit' (12 branches) at 0x7f8e8849c130>,
 <TTree 'opticalparam' (36 branches) at 0x7f8e88416cb0>,
 <TTree 'mu' (29 branches) at 0x7f8e88483fd0>,
 <TTree 'muIso' (30 branches) at 0x7f8e8834a7a0>,
 <TTree 'mufastn' (13 branches) at 0x7f8e883e4160>]
```

#### 操作TH

```Python
file["stepno;1"].to_hist()
```

![img](https://ezcjzah48j.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjBiOTQyMDU2ZDQ4ZTZkNjc4YTRjYjViMzA1ZmRmMGVfTE9RbXpaVFV5ZE1rcHZjNFFuYXQ4RGhQeTJyNFBvOWVfVG9rZW46SmtwR2JUQ0RjbzBPNGl4SmNJeWNqVEdmbmVoXzE3MDA3ODg5MjI6MTcwMDc5MjUyMl9WNA)

#### 操作TTree

```Python
mu_tree = file.get("mu")
mu_tree.keys()

------------------Output---------------------------
['evtID','MuMult','PDG', 'MuInitPosx', 'MuInitPosy', 'MuInitPosz', 'MuInitPx', 'MuInitPy', 
 'MuInitPz', 'MuInitKine', 'TrackLengthInRock', 'TrackLengthInVetoWater', 
 'TrackLengthInCDWater',
 'TrackLengthInAcrylic', 
 'TrackLengthInSteel',
 'TrackLengthInScint',
 'ELossInRock',
 'ELossInVetoWater',
 'ELossInCDWater',
 'ELossInAcrylic',
 'ELossInSteel',
 'ELossInScint',
 'MuExitPosx',
 'MuExitPosy',
 'MuExitPosz',
 'mustpMaterial',
 'mustpx',
 'mustpy',
 'mustpz']
mu_tree.values()

------------------Output---------------------------
[<TBranch 'evtID' at 0x7f8e8825e830>,
 <TBranch 'MuMult' at 0x7f8e8825efe0>,
 <TBranch 'PDG' at 0x7f8e8825f700>,
 <TBranch 'MuInitPosx' at 0x7f8e8825fe20>,
 <TBranch 'MuInitPosy' at 0x7f8e88278580>,
 <TBranch 'MuInitPosz' at 0x7f8e88278ca0>,
 <TBranch 'MuInitPx' at 0x7f8e882793c0>,
 <TBranch 'MuInitPy' at 0x7f8e88279ae0>,
 <TBranch 'MuInitPz' at 0x7f8e8827a200>,
 <TBranch 'MuInitKine' at 0x7f8e8827a920>,
 <TBranch 'TrackLengthInRock' at 0x7f8e8827b040>,
 <TBranch 'TrackLengthInVetoWater' at 0x7f8e8827b760>,
 <TBranch 'TrackLengthInCDWater' at 0x7f8e8827be80>,
 <TBranch 'TrackLengthInAcrylic' at 0x7f8e8828c5e0>,
 <TBranch 'TrackLengthInSteel' at 0x7f8e8828cd00>,
 <TBranch 'TrackLengthInScint' at 0x7f8e8828d420>,
 <TBranch 'ELossInRock' at 0x7f8e8828db40>,
 <TBranch 'ELossInVetoWater' at 0x7f8e8828e260>,
 <TBranch 'ELossInCDWater' at 0x7f8e8828e980>,
 <TBranch 'ELossInAcrylic' at 0x7f8e8828f0a0>,
 <TBranch 'ELossInSteel' at 0x7f8e8828f7c0>,
 <TBranch 'ELossInScint' at 0x7f8e8828fee0>,
 <TBranch 'MuExitPosx' at 0x7f8e882a4640>,
 <TBranch 'MuExitPosy' at 0x7f8e882a4d60>,
 <TBranch 'MuExitPosz' at 0x7f8e882a5480>,
 <TBranch 'mustpMaterial' at 0x7f8e882a5ba0>,
 <TBranch 'mustpx' at 0x7f8e882a62c0>,
 <TBranch 'mustpy' at 0x7f8e882a69e0>,
 <TBranch 'mustpz' at 0x7f8e882a7100>]
mu_tree.typenames()

------------------Output---------------------------
{'evtID': 'int32_t',
 'MuMult': 'int32_t',
 'PDG': 'int32_t[]',
 'MuInitPosx': 'double[]',
 'MuInitPosy': 'double[]',
 'MuInitPosz': 'double[]',
 'MuInitPx': 'double[]',
 'MuInitPy': 'double[]',
 'MuInitPz': 'double[]',
 'MuInitKine': 'double[]',
 'TrackLengthInRock': 'double[]',
 'TrackLengthInVetoWater': 'double[]',
 'TrackLengthInCDWater': 'double[]',
 'TrackLengthInAcrylic': 'double[]',
 'TrackLengthInSteel': 'double[]',
 'TrackLengthInScint': 'double[]',
 'ELossInRock': 'double[]',
 'ELossInVetoWater': 'double[]',
 'ELossInCDWater': 'double[]',
 'ELossInAcrylic': 'double[]',
 'ELossInSteel': 'double[]',
 'ELossInScint': 'double[]',
 'MuExitPosx': 'double[]',
 'MuExitPosy': 'double[]',
 'MuExitPosz': 'double[]',
 'mustpMaterial': 'int32_t[]',
 'mustpx': 'double[]',
 'mustpy': 'double[]',
 'mustpz': 'double[]'}
mu_tree.show()

------------------Output---------------------------
name                 | typename                 | interpretation                
---------------------+--------------------------+-------------------------------
evtID                | int32_t                  | AsDtype('>i4')
MuMult               | int32_t                  | AsDtype('>i4')
PDG                  | int32_t[]                | AsJagged(AsDtype('>i4'))
MuInitPosx           | double[]                 | AsJagged(AsDtype('>f8'))
MuInitPosy           | double[]                 | AsJagged(AsDtype('>f8'))
MuInitPosz           | double[]                 | AsJagged(AsDtype('>f8'))
MuInitPx             | double[]                 | AsJagged(AsDtype('>f8'))
MuInitPy             | double[]                 | AsJagged(AsDtype('>f8'))
MuInitPz             | double[]                 | AsJagged(AsDtype('>f8'))
MuInitKine           | double[]                 | AsJagged(AsDtype('>f8'))
TrackLengthInRock    | double[]                 | AsJagged(AsDtype('>f8'))
TrackLengthInVeto... | double[]                 | AsJagged(AsDtype('>f8'))
TrackLengthInCDWater | double[]                 | AsJagged(AsDtype('>f8'))
TrackLengthInAcrylic | double[]                 | AsJagged(AsDtype('>f8'))
TrackLengthInSteel   | double[]                 | AsJagged(AsDtype('>f8'))
TrackLengthInScint   | double[]                 | AsJagged(AsDtype('>f8'))
ELossInRock          | double[]                 | AsJagged(AsDtype('>f8'))
ELossInVetoWater     | double[]                 | AsJagged(AsDtype('>f8'))
ELossInCDWater       | double[]                 | AsJagged(AsDtype('>f8'))
ELossInAcrylic       | double[]                 | AsJagged(AsDtype('>f8'))
ELossInSteel         | double[]                 | AsJagged(AsDtype('>f8'))
ELossInScint         | double[]                 | AsJagged(AsDtype('>f8'))
MuExitPosx           | double[]                 | AsJagged(AsDtype('>f8'))
MuExitPosy           | double[]                 | AsJagged(AsDtype('>f8'))
MuExitPosz           | double[]                 | AsJagged(AsDtype('>f8'))
mustpMaterial        | int32_t[]                | AsJagged(AsDtype('>i4'))
mustpx               | double[]                 | AsJagged(AsDtype('>f8'))
mustpy               | double[]                 | AsJagged(AsDtype('>f8'))
mustpz               | double[]                 | AsJagged(AsDtype('>f8'))
mu_tree["MuInitKine"]
mu_tree["MuInitKine"].array()

------------------Output---------------------------
[[8.96e+04],
 [5.8e+05],
 [6.93e+04, 3.11e+05],
 [3.69e+03],
 [6.91e+05, 7.58e+04],
 ...,
 [7.26e+04],
 [2.21e+05],
 [4.36e+05, 4.24e+05, 2.06e+04],
 [9.37e+03],
 [1.84e+05]]
my_data = mu_tree.arrays(["TrackLengthInScint", "ELossInScint"])
my_data

------------------Output---------------------------
[{TrackLengthInScint: [0], ELossInScint: [0]},
 {TrackLengthInScint: [0], ELossInScint: [0]},
 {TrackLengthInScint: [1.27e+04], ELossInScint: [-2.4e+03]},
 {TrackLengthInScint: [0], ELossInScint: [0]},
 {TrackLengthInScint: [0, 0], ELossInScint: [0, 0]},
 {TrackLengthInScint: [2.18e+04], ELossInScint: [-4.61e+03]},
 {TrackLengthInScint: [0], ELossInScint: [0]},
 {TrackLengthInScint: [0], ELossInScint: [0]},
 {TrackLengthInScint: [0], ELossInScint: [0]},
 {TrackLengthInScint: [0, 0], ELossInScint: [0, 0]},
 ...,
 {TrackLengthInScint: [0], ELossInScint: [0]},
 {TrackLengthInScint: [3.09e+04], ELossInScint: [-1.16e+04]},
 {TrackLengthInScint: [0, 0, 0], ELossInScint: [0, ..., 0]},
 {TrackLengthInScint: [0], ELossInScint: [0]},
 {TrackLengthInScint: [0], ELossInScint: [0]},
 {TrackLengthInScint: [1.25e+04], ELossInScint: [-5.43e+03]},
 {TrackLengthInScint: [0], ELossInScint: [0]},
 {TrackLengthInScint: [0], ELossInScint: [0]},
 {TrackLengthInScint: [0], ELossInScint: [0]}]
-------------------------------------------------------------
type: 2997000 * {
    TrackLengthInScint: var * float64,
    ELossInScint: var * float64
}
mu_tree.arrays("sqrt(TrackLengthInScint**2 + ELossInScint**2)")

------------------Output---------------------------
[{'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [0]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [0]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [1.29e+04]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [0]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [0, 0]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [2.23e+04]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [0]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [0]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [0]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [0, 0]},
 ...,
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [0]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [3.3e+04]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [0, 0, 0]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [0]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [0]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [1.36e+04]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [0]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [0]},
 {'sqrt(TrackLengthInScint**2 + ELossInScint**2)': [0]}]
------------------------------------------------------------------
type: 2997000 * {
    "sqrt(TrackLengthInScint**2 + ELossInScint**2)": var * float64
}
```

#### uproot+plotly 绘图

[uproot+plotly 绘图](https://esword618.github.io/ROOT-project/html/uproot-py-1.html)

