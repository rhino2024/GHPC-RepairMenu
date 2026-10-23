# 载具维修菜单

Gunner, HEAT, PC! 的 MelonLoader 模组。在游戏自己的 Q 键菜单里加一个 Repair 子菜单，自己点要修哪一块，修一块只花一块的时间。

## 你会看到什么

原版只有一次性全修，点下去发动机、变速箱、散热器、两条履带一起恢复。这个模组把它拆开。

按 Q，菜单里多出一个 Repair，里面只列你这辆车当前真的坏掉的东西，每一项后面标着自己的秒数：

| 菜单项 | 全修 30 秒时占多少 |
| --- | --- |
| Repair/All | 30 |
| Engine | 8 |
| Transmission | 8 |
| Radiator | 4 |
| Left Track / Right Track | 各 5 |

项目名是英文，那是游戏自己的模块名，菜单排在游戏原生条目的位置、用游戏自己的字体和样式。

点一项就开始读条。屏幕底部写还剩几秒，那块模块的血量在读条期间一点点涨回来。中途再点一次同一项可以取消，已经修起来的部分不会退回去。RepairSeconds 填 0 就是原来那种瞬间修完。

时间走完才算修好，而且不是只把血量拉满：熄火的发动机重新打起来，被打烂的变速箱恢复成坏之前的挡位类型，断了电的车重新供电、炮塔平台照明亮起来，游戏里的伤害标志和伤害文字一起清掉。机动性不会提前放行，要等发动机和两条履带都好才解除底盘瘫痪与手刹，所以只修散热器不会让一辆断履带的车跑起来。

换过车、阵亡重新上岗、菜单被游戏重建之后，Repair 都还在。两辆同型车坏在相同的位置也不会共用一套菜单项。完全健康的车不会留下一个空的 Repair 子菜单。修车期间打开另一辆车的菜单，那一项写着 busy on another vehicle，不会让你同时开两份工。

不管三件事：外观凹陷不补，乘员不复活，弹药不加。

## 装

1. 先彻底退出游戏。游戏开着的时候 dll 是锁住的，覆盖不了。
2. 把 zip 解压到游戏根目录，就是放着 `GHPC.exe` 的那一层。解压出来应该看到 `Bin\Mods\RepairMenu.dll`。
3. 开一次游戏。MelonLoader 会在 `Bin\UserData\MelonPreferences.cfg` 里写出 `[RepairMenu]` 这一段。

需要 MelonLoader v0.7.2（net35 运行时），下载包里没有它。它不改游戏任何文件，删掉那个 dll 就算卸载。

## 能改的东西

| 名字 | 默认 | 作用 |
| --- | --- | --- |
| RepairSeconds | 30 | 全修的总时长，单项按自己的份数分；填 0 就是立刻修完 |
| ShowProgress | true | 屏幕底部那行剩余秒数 |
| DebugLog | false | 出问题再开，会写 `Bin/Mods/RepairMenu.debug.log` |

没有开关键，它只在你按 Q 的时候做事。

## 先说清楚

菜单里那个 Repair Kit（按 J 读条维修）跟这个模组功能重叠。两者一起装请只开一个，同时开着从来没验证过。

读条期间你还是能被击毁的，它不给你任何无敌。

## 想自己编译

不用 .NET SDK，也不用 Unity 编辑器，一个 dll 而已，用任何 Roslyn `csc` 对着游戏自带的托管程序集编就行：

```bash
GHPC_DIR="/path/to/Gunner HEAT PC/Bin" bash src/build.sh deploy
```

`deploy` 会把编出来的 dll 覆盖到 `<游戏目录>\Bin\Mods\`，所以先关游戏。不加 `deploy` 就只编到 `src/bin/`。

## In English

Adds a Repair submenu to the game's own Q context menu, so you pick which damaged module to fix instead of taking the all-or-nothing repair the game offers: Engine, Transmission, Radiator, Left Track, Right Track, each with its own seconds, thirty in total for a full job (RepairSeconds = 0 gives the instant fix back). Health climbs while the timer runs, the line at the bottom of the screen shows what is left, and clicking the same entry cancels without losing the part already repaired. Only when the timer finishes are the game's own damage flags, the stopped engine, the gearbox type, the power state and the turret platform restored, and the vehicle is only released from its broken state once the engine and both tracks are healthy.

MIT，与 Radian Simulations 无关。在当前 Steam 版上实测过，游戏更新有可能让它失效。
