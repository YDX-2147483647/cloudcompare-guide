# 从数据源导出合适格式

## 信息表示方式

CloudCompare 用序列表示点云，序列中每一项代表一点，每一点有空间坐标（x、y、z）和若干通道（如实部 real、虚部 imag）：

| x   | y   | z   | real  | imag  |
| --- | --- | --- | --- | --- |
| 0.5 | 0.9 | 0.3 | 5.2 | 1.9 |
| 0.3 | 0.7 | 1.0 | 9.3 | 7.4 |
| 0.7 | 0.9 | 0.8 | 5.2 | 7.6 |
| 0.3 | 0.6 | 0.9 | 7.2 | 3.8 |
| 0.2 | 0.8 | 0.1 | 5.9 | 6.4 |
| …   | …   | …   | …   | …   |

<style>
  table:nth-of-type(1) {
    th,
    td {
      &:nth-child(3) {
        border-right: solid darkgray;
      }
    }
  }
</style>

## 具体数据格式

[CloudCompare 支持几十种数据格式](https://www.cloudcompare.org/doc/wiki/index.php/FILE_I/O)，以下两种最简单，适合导出。

- **ASCII** / <abbr title="comma-separated values">CSV</abbr>

  - 文本格式，简单直观，但存储低效。
  - 无元数据，CloudCompare 打开时会弹出导入向导 _Open Ascii File_。（不必修改选项，直接 _Apply_ 即可。）
  - 文件名无明确规范，`*.txt`/`*.csv`/`*.xyz`等都可以。

  ```python
  0.5,0.9,0.3,5.2,1.9
  0.3,0.7,1.0,9.3,7.4
  0.7,0.9,0.8,5.2,7.6
  0.3,0.6,0.9,7.2,3.8
  0.2,0.8,0.1,5.9,6.4
  ```

- [**SBF**（simple binary format）](https://www.cloudcompare.org/doc/wiki/index.php/SBF)

  - 二进制格式，存储高效，但人难查看。
  - 分为文本元数据`*.sbf`和二进制数据`*.sbf.data`两个文件，CloudCompare 打开时选择任意一个即可。

  ```toml
  [SBF]
  Points=5
  GlobalShift=0.000000, 0.000000, 0.000000
  SFCount=2
  SF1=real
  SF2=imag
  ```

  ```
  2a2a0000 00000000 00050002
  00000000 00000000 00000000
  00000000 00000000 00000000 00000000 00000000
  00000000 00000000 00000000 00000000 00000000
  3f000000 3f666666 3e99999a 40a66666 3ff33333
  3e99999a 3f333333 3f800000 4114cccd 40eccccd
  3f333333 3f666666 3f4ccccd 40a66666 40f33333
  3e99999a 3f19999a 3f666666 40e66666 40733333
  3e4ccccd 3f4ccccd 3dcccccd 40bccccd 40cccccd
  ```

## 导出

下面将分技术栈介绍如何导出合适格式。

- [NumPy](./numpy.md)
- [MATLAB](./matlab.md)
