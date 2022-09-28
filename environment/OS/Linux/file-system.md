# 文件系统

## 挂载

- 磁盘分区

  将硬盘驱动器分为多个逻辑存储单元,它们被称为分区,来将一个物理磁盘驱动器视为多个磁盘

  > "分治"原则的应用, 流氓程序不能通过占用所有磁盘空间, 使整个服务器崩溃, 该程序将限制在其分区中

- 文件系统

  一种组织数据的手段

  > 类 Unix 操作系统创建一个虚拟文件系统,这使得所有设备上的所有文件似乎都存在于单个层次结构中.这意味着,在这些系统中,有一个根目录,系统上存在的每个文件位于它下方的某个地方.
  >
  > 所有文件系统都集成在一个大树中