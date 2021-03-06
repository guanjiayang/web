### 为什么要4K对齐？

- 容量拓展和读写能力，随着硬盘容量已经攀升，TB大小级别的高容量硬盘的普及，原来规定的每个扇区512字节不再合理，效率低了，于是将每个扇区512字节改为每个扇区4096个字节，也就是现在常说的“4K扇区”。

- 硬盘文件系统，随着NTFS成为了标准的硬盘文件系统，其文件系统的默认分配单元大小（簇）也是4096字节，为了使簇与扇区相对应，即使物理硬盘分区与计算机使用的逻辑分区对齐，保证硬盘读写效率，所以，有了“4K对齐”的概念。传统硬盘的每个扇区固定是512字节，新标准的"4K扇区"的硬盘，硬盘厂商为了保证与操作系统兼容性，也将扇区模拟成512B扇区，这时就会有4K扇区和4K簇不对齐的情况发生。

### 哪些需要4K对齐：

- 固态硬盘，对于固态硬盘来说，如果不对齐不但会极大的降低数据写入和读取速度，还会造成固态硬盘不必要的写入次数，而且寿命也会缩短。

- 采用Advanced Format的机械硬盘，这是因为在NTFS6.x 以前的规范中，数据的写入点正好会介于在两个4K扇区的之间，也就是说即使是写入最小量的数据，也会使用到两个4K扇区，这样造成跨区读写，读写次数放大，从而影响读写速度。

### 对齐方法定义：

- “4K对齐”就是将硬盘扇区对齐到8的整数倍个模拟扇区，即512B*8=4096B，4096字节即是4K。所以只要是8的倍数都是4K对齐了。

- 所谓“4K对齐”就是符合“4K扇区”定义格式化过的硬盘，并且按照“4K 扇区”的规则写入数据。
