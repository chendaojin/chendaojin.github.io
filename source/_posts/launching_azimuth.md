---
title: 发射方位角计算
date: 2019-11-05 15:00
updated: 2019-11-05 16:00
tags: [proj.4]
categories: 技术
mathjax: true
description: 基于墨卡托投影计算发射方位角
---

# 发射方位角

- 描述：计算北纬、东经下的发射方位角
- 输入：发射点经度、纬度、高度，打击点经度、纬度、高度(单位为DEG)
- 输出：发射方位角，顺时针为正
- 基本思路：基于proj.4将发射点和打击点坐标转化到墨卡托投影下的坐标，并构造一条真北方向向量，二者之间夹角为发射方位角

```c++
#include <proj_api.h>

double get_launching_azimuth(double f_ld, double f_bd, double f_h,
	double i_ld, double i_bd, double i_h){

	std::string str = " +proj=tmerc +lat_0=" + std::to_string(f_bd / 2 + i_bd / 2) +
		" +lon_0=" + std::to_string(f_ld / 2 + i_ld / 2) + " +k_0=1" 
		" +x_0=3500000 +y_0=0 +ellps=bessel"
		" +datum=potsdam +units=m +no_defs";
	printf("proj.4 string: %s\n", str.c_str());

	const int sign = f_ld <= i_ld ? 1 : -1;
	double n_ld = f_ld * DEG_TO_RAD;
	double n_bd = (f_bd + 1) * DEG_TO_RAD;
	f_ld *= DEG_TO_RAD;
	f_bd *= DEG_TO_RAD;
	i_ld *= DEG_TO_RAD;
	i_bd *= DEG_TO_RAD;
	projPJ PJ_WGS = pj_init_plus(str.c_str());
	projUV parr[3] = {
			{ f_ld, f_bd }, //发射点
			{ i_ld, i_bd },  //打击点
			{ n_ld, n_bd } //大地北
	};
	projUV p0 = pj_fwd(parr[0], PJ_WGS);
	printf("发射点投影  坐标:%10lf,%10lf\n", p0.u, p0.v);
	projUV p1 = pj_fwd(parr[1], PJ_WGS);
	printf("打击点投影  坐标:%10lf,%10lf\n", p1.u, p1.v);
	projUV p2 = pj_fwd(parr[2], PJ_WGS);
	printf("大地北投影  坐标:%10lf,%10lf\n", p2.u, p2.v);

	double north[] = { p2.u - p0.u, p2.v - p0.v };
	double direction[] = { p1.u - p0.u, p1.v - p0.v };
	printf("正北方向向量: (%lf, %lf)\n", north[0], north[1]);
	printf("发射指向向量: (%lf, %lf)\n", direction[0], direction[1]);

	double dot = north[0] * direction[0] + north[1] * direction[1];
	double norm_a = sqrt(pow(north[0], 2) + pow(north[1], 2));
	double norm_b = sqrt(pow(direction[0], 2) + pow(direction[1], 2));

	double A = sign * acos(dot / (norm_a*norm_b)) * RAD_TO_DEG;
	printf("方位角: %.5lf\n", A);
	return A;
}
```

- 测试样例：

  单位：经度(deg)，纬度(deg)，高度(m)，方位角(deg)

  |       发射点       |       打击点       | 方位角（deg） |
  | ---------------- | ---------------- | ----------- |
  | 97.67, 33.13, 1000 | 98.67, 33.13, 1000 |   89.72308    |
  | 97.67, 33.13, 1000 | 97.67, 34.13, 1000 |    0.0000     |
  | 97.67, 33.13, 1000 | 97.67, 32.13, 1000 |    180.000    |
  | 98.67, 33.13, 1000 | 97.67, 33.13, 1000 |   -89.72308   |

  

- 参考资料：

  [[1]proj.4高斯-克吕格转化](https://proj.org/operations/projections/tmerc.html)

  [[2]周立锋,曹淑艳.基于高斯投影的发射方位角精确计算方法[J].兵工自动化,2015,34(05):5-6+10.](https://kns.cnki.net/kns/ViewPage/viewsave.aspx?t=1572943166347)

  [[3]proj.4参数](https://proj.org/usage/projections.html)