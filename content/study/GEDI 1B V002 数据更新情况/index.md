---
title: 'GEDI 1B V002 数据更新情况'

subtitle: 'GEDI 1B 数据更新的主要情况'

summary: Create a beautifully simple website in under 10 minutes.

authors:
- admin
tags:
- Academic
categories:
- Academic
math: true
diagram: true
# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Placement options: 1 = Full column width, 2 = Out-set, 3 = Screen-width
# Focal point options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
image:
  placement: 2
  focal_point: ""
  preview_only: false
---



[TOC]

------



# 数据更新情况

## 前言

在2021年4月30号左右，发布了GEDI 1B/2A/2B V002的数据，当时五月份的时候知道有这个事情，但是因为一直忙于自己的一维残差网络数据处理情况，没怎么看这个数据是怎么更新得，当我发现了[The impact of geolocation uncertainty on GEDI tropical forest canopy height estimation and change monitoring](https://doi.org/10.1016/j.srs.2021.100024)的时候，看见对GEDI数据定位偏差分析的结果部分，讨论了关于V002数据集的定位精度，才发现这个更新版本的数据和之前的数据集定位有了较为明显的提高，看了一下说明书，了解一下主要的变化

## 主要变化

![data progress](/1.png)

这个文档历史主要存在于2.0和2.1数据，2.1的**Addtion of Known Issues**是最为重要的一点

## 版本2 L1B的重要产品说明

>  The L1B product contains all geolocated return waveforms. The L1B product provides corrected geolocated waveform returns, including transmit and receive housekeeping and relevant instrument parameters, as well as geolocation parameters and geophysical corrections. At the processing level of the L1B  product, the waveform returns have not been filtered nor has noise  characterization been conducted to determine if a valid land surface return exists.   GEDI Version 2 data product improvements include improved geolocation  accuracy, updates to the metadata to provide spatial coordinates that allow  querying in NASA Earthdata Search, and a reduction in granule size from one full  ISS orbit to four segments per orbit. A full list of changes and filename convention  details are provided in section 7 of this document. The Version 2 filenames have  also been updated to include segment number and version number. The filename  convention details are provided in section 2.1.4 of this document. 



​	L1B产品包含所有地理定位返回波形。L1B产品提供校正的地理定位波形返回，包括发射和接收内务处理和相关仪器参数，以及地理定位参数和地球物理校正。在L1B产品的处理级别，波形回波没有经过滤波，也没有进行噪声表征来确定是否存在有效的地表回波。**GEDI第二版数据产品的改进包括提高地理定位精度，更新元数据以提供允许在美国航天局地球数据搜索中查询的空间坐标，以及将粒子大小从一个完整的国际空间站轨道减少到每个轨道四个片段。**本文档第7节提供了更改和文件名约定详细信息的完整列表。版本2文件名也已更新，包括段号和版本号。文件名约定的详细信息在本文档的第2.1.4节中提供。

​	由此可见主要变更的为这个3个方面：

1. **提高了地理定位精度**
2. **更新了原数据在Earth Data 中查询能力**
3. **一个长轨道被分为四个小轨道**

------

三个变化具体说明体现如下：

### 命名编号的命名改变

<img src="/2.png" alt="name rules" style="zoom:50%;" />

主要的变化是加入的Sub-orbit Granule Number的编号，一份化为4段

### 改进的地理定位

> Improved geolocation: V002 mean 1-sigma horizontal geolocation error is 10.2 m 
> with 95% of the mission weeks having 1-sigma geolocation error less than 13.2 
> m.  In comparison V001 mean 1-sigma horizontal geolocation error is 23.8 m with 
> 95% of the mission weeks having 1-sigma geolocation error less than 27.2 m 
> (from the analysis of Mission Weeks 19 through 50). 

- 通过对激光相对光束对准、时变激光帧对准的全面校准，以及对距离偏差的改进估计，V002水平地理定位误差得到了显著改善。当前的V002平均1σ水平地理定位误差为10.2米，95%的任务周的1σ地理定位误差小于13.2米。虽然V002水平地理定位误差比V001提高了2倍以上，但分析表明，在未来的版本中，地理定位将进一步提高。通过对已知表面的直接测高、与独立数据的比较和交叉分析，对距离/高度性能进行了评估。基本的仪器测距精度在3厘米左右。
- 改进的激光信道相关距离偏差估计和激光距离跟踪点建模已经校正了在版本V001中观察到的  -56 cm距离/仰角偏差。版本V002高程误差现在主要由倾斜表面上的水平误差(相对于表面的激光入射角)的贡献决定。例如，10.2米1σ水平地理定位误差在1度坡度(激光表面入射角)上引起17.8cm的高度误差。

------

# 质量和重要注意事项

这段我觉得是这篇文章的主题，作为用户最为关心的一点就是数据的质量和使用情况

> - The Level 1B product is intended for users who are interested in analyzing the entire  return waveform themselves.  Most users should start with the Level 2 data files. The  Level 1B geolocated waveforms provide context and source data for the GEDI Level 2  products that will allow the expert user to replicate or derive new geolocated Level 2 data  products using different algorithms and methodologies for ground and feature finding.  There are numerous time periods where the geolocation performance suffers due to non- optimal operating conditions. These situations include blinding or glinting of one or more  instrument star trackers. The “degrade” dataset in the “geolocation” group provides an  indication of when there is degraded geolocation. The “degrade” flag is a best estimate  of these time periods and data could be performing better or worse in the surrounding  time periods near the start and stop of the “degrade” flagged intervals. The “degrade” flag  should be understood as a general indicator of a potential issue.    
> - The first (elevation_bin0) and last (elevation_lastbin) return in the waveform are  geolocated. To compute the geolocation of any point in the waveform (e.g. ground return),  the user would interpolate the first and last return geolocation to the waveform location of  interest. This is done in the L2 products where the geolocation of the ground return and  other waveform metrics are provided. 
> - **The L1B product geolocation group contains several “error”  datasets (i.e.  latitude_lastbin_error). These formal propagated errors have not yet been fully calibrated.  Their relative magnitude is a good indicator of relative geolocation quality, but their  absolute magnitudes should not be interpreted as the actual geolocation error at this time.**  Future releases will contain calibrated geolocation “error” datasets that then can be used  for an estimate of absolute error.   The user is encouraged to read section 3.7 of the ATBD for GEDI Waveform Geolocation  for L1 and L2 Products to fully understand the application of the geophysical corrections.  Of special note: The ellipsoid height of bounce points within the /geolocation group  (elevation_bin0 and elevation_lastbin) has been corrected for solid earth tides,  ocean loading, solid earth pole tide, and ocean pole tide. The bounce points are NOT  corrected for ocean tides and dynamic atmospheric correction. These corrections are  applied by subtracting the corrections from the bounce point elevations. To remove the  corrections already applied (restore the geophysical signal of interest), corrections need  to be added to the bounce point elevations.    For complete and updated information regarding product quality, see the  GEDI Mission Website. 

- Level 1B产品面向对自己分析整个回波波形感兴趣的用户。大多数用户应该从2级数据文件开始。1B级地理定位波形为GEDI 2级产品提供背景和源数据，**这将允许专家用户使用不同的算法和方法复制或导出新的地理定位2级数据产品，用于地面和特征寻找。**
- 由于非最佳操作条件，有许多时间段地理定位性能会受到影响。这些情况包括一个或多个仪表星跟踪器变瞎或闪烁。**“地理位置”组中的“降级”数据集提供了何时存在降级地理位置的指示。“降级”标志是对这些时间段的最佳估计，并且在“降级”标志间隔的开始和停止附近的周围时间段中，数据可能表现得更好或更差。**“降级”标志应理解为潜在问题的一般指示。波形中的第一个(elevation_bin0)和最后一个(elevation_lastbin)返回是地理定位的。为了计算波形中任何点的地理位置(例如地面回波)，用户将第一次和最后一次回波地理位置插值到感兴趣的波形位置。这是在L2产品中完成的，其中提供了地面回波的地理位置和其他波形度量。
- **L1B产品地理定位组包含几个“错误”数据集(即latitude_lastbin_error)。**这些形式传播的误差尚未完全校准。它们的相对大小是相对地理定位质量的良好指标，但它们的绝对大小不应被解释为此时的实际地理定位误差。未来的版本将包含校准的地理定位“误差”数据集，然后可以用于估计绝对误差。
- 鼓励用户阅读《L1和L2产品的GEDI波形地理定位ATBD》第3.7节，以充分理解地球物理校正的应用。特别值得注意的是:在/地理定位组(elevation_bin0和elevation_lastbin)内反弹点的椭球高度已经针对固体地球潮汐、海洋载荷、固体地球极点潮汐和海洋极点潮汐进行了校正。海洋潮汐和动态大气校正不校正反弹点。这些校正通过从反弹点高程中减去校正来应用。要移除已经应用的校正(恢复感兴趣的地球物理信号)，需要将校正添加到反弹点高程。有关产品质量的完整和最新信息，请访问GEDI代表团网站。
