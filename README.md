# 提取推特地理信息
[中文](#提取推特地理信息)  [Eng](#extract-geodata-from-twitter)  

推特API直接提取的地理数据通常有限（仅限于当用户分享定位的情况）。
Mikael Brunila提供了一种从推特中提取到更多地理数据的方法：[戳这里](http://www.mikaelbrunila.fi/2017/03/27/scraping-extracting-mapping-geodata-twitter/)

其方法大致如下：
* 直接获取推文的定位信息（坐标或定位标签）
* 从用户的账号信息里提取

</br>

在Mikael的方法获得的数据基础上，可经过进一步清洗和整理得到所需的地理数据。
这里以提取伦敦市镇的地理信息为例（代码见“Twitter_Location.ipynb"）。

</br>


### 原理 
由前一步得到的地理数据（储存在”primary_geo"一栏）可分为以下几种类型：
1. 发推地点的具体坐标定位
2. 推文的地点标签
3. 用户账号信息里填写的地点信息

### 方法
1. 检查“primary_geo”的地理数据，如果是城市名，则记下该城市
2. 如果是街区名，则记下该街区所在的城市
3. 如果是具体地点，则通过地理编码API获取对应的坐标点
4. 判断点与Spatial Polygon的位置关系，将具体坐标点对应到市镇，排除伦敦边界外的地点和不明确的地点

</br>
</br>


# Extract Geodata from Twitter
Twitter API doesn't provide much information about geo-location of tweets.
Yet Mikael Brunila proposed a methodology to extract more geodata from twitter：[Click here](http://www.mikaelbrunila.fi/2017/03/27/scraping-extracting-mapping-geodata-twitter/)  

In which he scrapes two types of location data from twitter:
1. Exact location data for the tweet
2. General location data for the user.

Based on his methods, we can extract certain level of geo-location data. Here we will give an example and retrieve borough data from the tweets.

### THEORY
Borough locations will be extracted from the "primary_geo" column. The values in "primary_geo" are basically:  
1. the exact coordinates from where the tweet was created,
2. place tags the user chose from a list of candidate Twitter Places when they tweeted,
3. or locations provided in the user profile

### METHOD
1. Check the address in "primary_geo", if a borough is mentioned, store the borough name
2. If an area is mentioned, store the borough it is referenced to
3. If it's a specific place, return the coordinates using public geocoding API
4. Finally, assign the coordinate points with boroughs and exclued points with unclear locations or located out of London boundary 

