/*: 作者:第四梦境
 * 六种碰撞检测算法实现，MIT协议发布，即可以商用、可以修改
 *
 */
//**碰撞检测代码组S**\\

//三角形与三角形的碰撞检测
function isTOT (t1,t2) {
	var txls = [[],[]]; var czxls = [[[],[],[]],[[],[],[]]];
	txls[0] = [[t1[2] - t1[0],t1[3] - t1[1]],[t1[4] - t1[2],t1[5] - t1[3]],[t1[0] - t1[4],t1[1] - t1[5]]];
	txls[1] = [[t2[2] - t2[0],t2[3] - t2[1]],[t2[4] - t2[2],t2[5] - t2[3]],[t2[0] - t2[4],t2[1] - t2[5]]];
	
	//获取垂直向量
	for (var i = 0; i < 2; i++) {
		for (var j = 0; j < 3; j++) {
			czxls[i][j] = [-txls[i][j][1],txls[i][j][0]];
			//如果为零向量，将其方向坍缩
			if (Math.pow(czxls[i][j][0],2) + Math.pow(czxls[i][j][1],2) == 0) czxls[i][j] = [1,0];
		}
	}
	
	//如果三个垂直向量共线，则将其中一个转90°
	for (var i = 0; i < 2; i++) {
		if (czxls[i][1][0]*czxls[i][0][1] - czxls[i][0][0]*czxls[i][1][1] == 0 && czxls[i][1][0]*czxls[i][2][1] - czxls[i][2][0]*czxls[i][1][1] == 0) {
			czxls[i][1] = [-czxls[i][1][1],czxls[i][1][0]];
		}
	}
	
	//检测碰撞(分离轴)
	for (var i = 0; i < 2; i++) {
		for (var j = 0; j < 3; j++) {
			var d1,min1,max1;
			min1 = max1 = czxls[i][j][0] * t1[0] + czxls[i][j][1] * t1[1];
			d1 = czxls[i][j][0] * t1[2] + czxls[i][j][1] * t1[3];
			min1 = d1 < min1 ? d1 : min1;
			max1 = d1 > max1 ? d1 : max1;
			d1 = czxls[i][j][0] * t1[4] + czxls[i][j][1] * t1[5];
			min1 = d1 < min1 ? d1 : min1;
			max1 = d1 > max1 ? d1 : max1;
			
			var d2,min2,max2;
			min2 = max2 = czxls[i][j][0] * t2[0] + czxls[i][j][1] * t2[1];
			d2 = czxls[i][j][0] * t2[2] + czxls[i][j][1] * t2[3];
			min2 = d2 < min2 ? d2 : min2;
			max2 = d2 > max2 ? d2 : max2;
			d2 = czxls[i][j][0] * t2[4] + czxls[i][j][1] * t2[5];
			min2 = d2 < min2 ? d2 : min2;
			max2 = d2 > max2 ? d2 : max2;
			
			var rs = min1 < min2 ? min2 - max1 : min1 - max2;
			if (rs > 0) return false;
		}
	}
	return true;
};

//三角形与旋转矩形的碰撞检测
function isTOR (t,ro,cx,cy,hw,hh) {
	var txls = [[],[],[]]; var czxls = [[],[],[],[],[]];var sra = Math.sin(ro); var cra = Math.cos(ro);
	txls = [[t[2] - t[0],t[3] - t[1]],[t[4] - t[2],t[5] - t[3]],[t[0] - t[4],t[1] - t[5]]];
	
	//求hh和hw的水平分量和垂直分量
	var hwox  = hw * cra; var hwoy = hw * sra;
	var hhox  = hh * -sra; var hhoy = hh * cra;

	//求矩形四条边的中心点坐标
	var zxd0x = cx - hwox; var zxd0y = cy - hwoy;
	var zxd1x = cx - hhox; var zxd1y = cy - hhoy;
	var zxd2x = cx + hwox; var zxd2y = cy + hwoy;
	var zxd3x = cx + hhox; var zxd3y = cy + hhoy;
	
	//求矩形四个顶点的坐标
	var dd0x = zxd1x - hwox; var dd0y = zxd1y - hwoy;
	var dd1x = zxd1x + hwox; var dd1y = zxd1y + hwoy;
	var dd2x = zxd3x + hwox; var dd2y = zxd3y + hwoy;
	var dd3x = zxd3x - hwox; var dd3y = zxd3y - hwoy;
	
	//获取垂直向量
	for (var i = 0; i < 3; i++) {
		czxls[i] = [-txls[i][1],txls[i][0]];
		//如果为零向量，将其方向坍缩
		if (Math.pow(czxls[i][0],2) + Math.pow(czxls[i][1],2) == 0) czxls[i] = [1,0];
	}
	czxls[3] = [cra,sra];czxls[4] = [-sra,cra];
	
	//如果三个垂直向量共线，则将其中一个转90°
	if (czxls[1][0]*czxls[0][1] - czxls[0][0]*czxls[1][1] == 0 && czxls[1][0]*czxls[2][1] - czxls[2][0]*czxls[1][1] == 0) {
		czxls[1] = [-czxls[1][1],czxls[1][0]];
	}
	
	//检测碰撞(分离轴)
	for (var i = 0; i < 5; i++) {
		var d1,min1,max1;
		min1 = max1 = czxls[i][0] * t[0] + czxls[i][1] * t[1];
		d1 = czxls[i][0] * t[2] + czxls[i][1] * t[3];
		min1 = d1 < min1 ? d1 : min1;
		max1 = d1 > max1 ? d1 : max1;
		d1 = czxls[i][0] * t[4] + czxls[i][1] * t[5];
		min1 = d1 < min1 ? d1 : min1;
		max1 = d1 > max1 ? d1 : max1;
		
		var d2,min2,max2;
		min2 = max2 = czxls[i][0] * dd0x + czxls[i][1] * dd0y;
		d2 = czxls[i][0] * dd1x + czxls[i][1] * dd1y;
		min2 = d2 < min2 ? d2 : min2;
		max2 = d2 > max2 ? d2 : max2;
		d2 = czxls[i][0] * dd2x + czxls[i][1] * dd2y;
		min2 = d2 < min2 ? d2 : min2;
		max2 = d2 > max2 ? d2 : max2;
		d2 = czxls[i][0] * dd3x + czxls[i][1] * dd3y;
		min2 = d2 < min2 ? d2 : min2;
		max2 = d2 > max2 ? d2 : max2;
		
		var rs = min1 < min2 ? min2 - max1 : min1 - max2;
		if (rs > 0) return false;
	}
	return true;
};

//三角形与圆形的碰撞检测
function isTOC (t,x,y,r) {
	var txls = [[],[],[]]; var czxls = [[],[],[],[]]; var lyxzjd = [t[0],t[1]];
	txls = [[t[2] - t[0],t[3] - t[1]],[t[4] - t[2],t[5] - t[3]],[t[0] - t[4],t[1] - t[5]]];
	
	//获取垂直向量
	for (var i = 0; i < 3; i++) {
		czxls[i] = [-txls[i][1],txls[i][0]];
		if (Math.pow(czxls[i][0],2) + Math.pow(czxls[i][1],2) == 0) czxls[i] = [1,0];
	}
	lyxzjd = Math.pow(x - t[2],2) + Math.pow(y - t[3],2) < Math.pow(x - lyxzjd[0],2) + Math.pow(y - lyxzjd[1],2) ? [t[2],t[3]] : lyxzjd;
	lyxzjd = Math.pow(x - t[4],2) + Math.pow(y - t[5],2) < Math.pow(x - lyxzjd[0],2) + Math.pow(y - lyxzjd[1],2) ? [t[4],t[5]] : lyxzjd;
	czxls[3] = [x - lyxzjd[0],y - lyxzjd[1]];
	if (Math.pow(czxls[3][0],2) + Math.pow(czxls[3][1],2) == 0) return true;
	
	//如果三个垂直向量共线，则将其中一个转90°
	if (czxls[1][0]*czxls[0][1] - czxls[0][0]*czxls[1][1] == 0 && czxls[1][0]*czxls[2][1] - czxls[2][0]*czxls[1][1] == 0) {
		czxls[1] = [-czxls[1][1],czxls[1][0]];
	}
	
	//检测碰撞(分离轴)
	for (var i = 0; i < 4; i++) {
		var d1,min1,max1;
		min1 = max1 = czxls[i][0] * t[0] + czxls[i][1] * t[1];
		d1 = czxls[i][0] * t[2] + czxls[i][1] * t[3];
		min1 = d1 < min1 ? d1 : min1;
		max1 = d1 > max1 ? d1 : max1;
		d1 = czxls[i][0] * t[4] + czxls[i][1] * t[5];
		min1 = d1 < min1 ? d1 : min1;
		max1 = d1 > max1 ? d1 : max1;
		
		var min2 = czxls[i][0] * x + czxls[i][1] * y - r * Math.sqrt((Math.pow(czxls[i][0],2) + Math.pow(czxls[i][1],2)));
		var max2 = czxls[i][0] * x + czxls[i][1] * y + r * Math.sqrt((Math.pow(czxls[i][0],2) + Math.pow(czxls[i][1],2)));
		
		
		var rs = min1 < min2 ? min2 - max1 : min1 - max2;
		if (rs > 0) return false;
	}
	return true;
};

//旋转矩形与旋转矩形的碰撞检测
function isROR (tsro,tsbcx,tsbcy,tshw,tshh,tero,tebcx,tebcy,tehw,tehh) {
	var cdv = [tsbcx - tebcx, tsbcy - tebcy];
	var cros = [Math.cos(tsro),Math.cos(tsro + Math.PI / 2),Math.cos(tero),Math.cos(tero + Math.PI / 2)]
	var sros = [Math.sin(tsro),Math.sin(tsro + Math.PI / 2),Math.sin(tero),Math.sin(tero + Math.PI / 2)]
	
	for (var i = 0; i < 4; i++) {
		var tspax = Math.abs(cros[i] * cros[0] + sros[i] * sros[0]);
        var tspay = Math.abs(cros[i] * -sros[0] + sros[i] * cros[0]);
		var tepax = Math.abs(cros[i] * cros[2] + sros[i] * sros[2]);
        var tepay = Math.abs(cros[i] * -sros[2] + sros[i] * cros[2]);
		
		if(tshw * tspax + tshh * tspay + tehw * tepax + tehh * tepay <
		Math.abs(cdv[0] * cros[i] + cdv[1] * sros[i])) 
		{
			return false;
		}
	}
	return true;
};

//旋转矩形与圆形的碰撞检测
function isROC (ro,cx,cy,hw,hh,x,y,r) {
	var sra = Math.sin(-ro); var cra = Math.cos(-ro);
	var yx = cx + (x - cx) * cra - (y - cy) * sra;
	var yy = cy + (x - cx) * sra + (y - cy) * cra;
	var tx = yx < cx - hw ? cx - hw : yx > cx + hw ? cx + hw : yx;
	var ty = yy < cy - hh ? cy - hh : yy > cy + hh ? cy + hh : yy;
	tx -= yx;
	ty -= yy;
	return tx * tx + ty * ty < r * r;
};

//圆形与圆形的碰撞检测
function isCOC (x1,y1,r1,x2,y2,r2) {
	return Math.pow(x1 - x2,2) + Math.pow(y1 - y2,2) < Math.pow(r1 + r2,2);
};


//**碰撞检测代码组E**\\
