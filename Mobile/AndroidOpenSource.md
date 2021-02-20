# 开源库

## UI

+ [悬浮窗](https://github.com/yhaolpz/FloatWindow)

## 数据库

+ [Room](open_code/Room.md)

## 工具库

+ [非常好用的工具库](https://github.com/Blankj/AndroidUtilCode)

### 经纬度转换

```java
/**
 * 将百度坐标转换成GPS坐标工具类
 * <p>
 * 参考
 * https://www.cnblogs.com/fuyinshan/p/6733459.html
 * https://blog.csdn.net/yingtian648/article/details/79000331
 * https://github.com/taoweiji/JZLocationConverter-for-Android
 * <p>
 * 高德和谷歌国内使用火星坐标，国外使用wgs84
 * 百度国内使用BD-09坐标,国外使用wgs84
 */
public class LocationUtil {
    public final static double a = 6378245.0;
    private final static double ee = 0.00669342162296594323;

    private static double LAT_OFFSET_0(double x, double y) {
        return -100.0 + 2.0 * x + 3.0 * y + 0.2 * y * y + 0.1 * x * y + 0.2 * Math.sqrt(Math.abs(x));
    }

    private static double LAT_OFFSET_1(double x, double y) {
        return (20.0 * Math.sin(6.0 * x * Math.PI) + 20.0 * Math.sin(2.0 * x * Math.PI)) * 2.0 / 3.0;
    }

    private static double LAT_OFFSET_2(double x, double y) {
        return (20.0 * Math.sin(y * Math.PI) + 40.0 * Math.sin(y / 3.0 * Math.PI)) * 2.0 / 3.0;
    }

    private static double LAT_OFFSET_3(double x, double y) {
        return (160.0 * Math.sin(y / 12.0 * Math.PI) + 320 * Math.sin(y * Math.PI / 30.0)) * 2.0 / 3.0;
    }

    private static double LON_OFFSET_0(double x, double y) {
        return 300.0 + x + 2.0 * y + 0.1 * x * x + 0.1 * x * y + 0.1 * Math.sqrt(Math.abs(x));
    }

    private static double LON_OFFSET_1(double x, double y) {
        return (20.0 * Math.sin(6.0 * x * Math.PI) + 20.0 * Math.sin(2.0 * x * Math.PI)) * 2.0 / 3.0;
    }

    private static double LON_OFFSET_2(double x, double y) {
        return (20.0 * Math.sin(x * Math.PI) + 40.0 * Math.sin(x / 3.0 * Math.PI)) * 2.0 / 3.0;
    }

    private static double LON_OFFSET_3(double x, double y) {
        return (150.0 * Math.sin(x / 12.0 * Math.PI) + 300.0 * Math.sin(x / 30.0 * Math.PI)) * 2.0 / 3.0;
    }

    private static final double RANGE_LON_MAX = 137.8347;
    private static final double RANGE_LON_MIN = 72.004;
    private static final double RANGE_LAT_MAX = 55.8271;
    private static final double RANGE_LAT_MIN = 0.8293;

    private static final double jzA = 6378245.0;
    private static final double jzEE = 0.00669342162296594323;

    private static double transformLat(double x, double y) {
        double ret = LAT_OFFSET_0(x, y);
        ret += LAT_OFFSET_1(x, y);
        ret += LAT_OFFSET_2(x, y);
        ret += LAT_OFFSET_3(x, y);
        return ret;
    }

    private static double transformLon(double x, double y) {
        double ret = LON_OFFSET_0(x, y);
        ret += LON_OFFSET_1(x, y);
        ret += LON_OFFSET_2(x, y);
        ret += LON_OFFSET_3(x, y);
        return ret;
    }

    public static boolean outOfChina(double lat, double lon) {
        if (lon < RANGE_LON_MIN || lon > RANGE_LON_MAX)
            return true;
        if (lat < RANGE_LAT_MIN || lat > RANGE_LAT_MAX)
            return true;
        return false;
    }

    private static LatLng gcj02Encrypt(double ggLat, double ggLon) {
        LatLng resPoint = new LatLng();
        double mgLat;
        double mgLon;
        if (outOfChina(ggLat, ggLon)) {
            resPoint.latitude = ggLat;
            resPoint.longitude = ggLon;
            return resPoint;
        }
        double dLat = transformLat(ggLon - 105.0, ggLat - 35.0);
        double dLon = transformLon(ggLon - 105.0, ggLat - 35.0);
        double radLat = ggLat / 180.0 * Math.PI;
        double magic = Math.sin(radLat);
        magic = 1 - jzEE * magic * magic;
        double sqrtMagic = Math.sqrt(magic);
        dLat = (dLat * 180.0) / ((jzA * (1 - jzEE)) / (magic * sqrtMagic) * Math.PI);
        dLon = (dLon * 180.0) / (jzA / sqrtMagic * Math.cos(radLat) * Math.PI);
        mgLat = ggLat + dLat;
        mgLon = ggLon + dLon;

        resPoint.latitude = mgLat;
        resPoint.longitude = mgLon;
        return resPoint;
    }

    private static LatLng gcj02Decrypt(double gjLat, double gjLon) {
        LatLng gPt = gcj02Encrypt(gjLat, gjLon);
        double dLon = gPt.longitude - gjLon;
        double dLat = gPt.latitude - gjLat;
        LatLng pt = new LatLng();
        pt.latitude = gjLat - dLat;
        pt.longitude = gjLon - dLon;
        return pt;
    }

    private static LatLng bd09Decrypt(double bdLat, double bdLon) {
        LatLng gcjPt = new LatLng();
        double x = bdLon - 0.0065, y = bdLat - 0.006;
        double z = Math.sqrt(x * x + y * y) - 0.00002 * Math.sin(y * Math.PI);
        double theta = Math.atan2(y, x) - 0.000003 * Math.cos(x * Math.PI);
        gcjPt.longitude = z * Math.cos(theta);
        gcjPt.latitude = z * Math.sin(theta);
        return gcjPt;
    }

    private static LatLng bd09Encrypt(double ggLat, double ggLon) {
        LatLng bdPt = new LatLng();
        double x = ggLon, y = ggLat;
        double z = Math.sqrt(x * x + y * y) + 0.00002 * Math.sin(y * Math.PI);
        double theta = Math.atan2(y, x) + 0.000003 * Math.cos(x * Math.PI);
        bdPt.longitude = z * Math.cos(theta) + 0.0065;
        bdPt.latitude = z * Math.sin(theta) + 0.006;
        return bdPt;
    }

    /**
     * @param location 世界标准地理坐标(WGS-84)
     * @return 中国国测局地理坐标（GCJ-02）<火星坐标>
     * @brief 世界标准地理坐标(WGS - 84) 转换成 中国国测局地理坐标（GCJ-02）<火星坐标>
     * <p>
     * ####只在中国大陆的范围的坐标有效，以外直接返回世界标准坐标
     */
    public static LatLng wgs84ToGcj02(LatLng location) {
        return gcj02Encrypt(location.latitude, location.longitude);
    }

    /**
     * @param location 中国国测局地理坐标（GCJ-02）
     * @return 世界标准地理坐标（WGS-84）
     * @brief 中国国测局地理坐标（GCJ-02） 转换成 世界标准地理坐标（WGS-84）
     * <p>
     * ####此接口有1－2米左右的误差，需要精确定位情景慎用
     */
    public static LatLng gcj02ToWgs84(LatLng location) {
        return gcj02Decrypt(location.latitude, location.longitude);
    }

    /**
     * @param location 世界标准地理坐标(WGS-84)
     * @return 百度地理坐标（BD-09)
     * @brief 世界标准地理坐标(WGS - 84) 转换成 百度地理坐标（BD-09)
     */
    public static LatLng wgs84ToBd09(LatLng location) {
        LatLng gcj02Pt = gcj02Encrypt(location.latitude, location.longitude);
        return bd09Encrypt(gcj02Pt.latitude, gcj02Pt.longitude);
    }

    /**
     * @param location 中国国测局地理坐标（GCJ-02）<火星坐标>
     * @return 百度地理坐标（BD-09)
     * @brief 中国国测局地理坐标（GCJ-02）<火星坐标> 转换成 百度地理坐标（BD-09)
     */
    public static LatLng gcj02ToBd09(LatLng location) {
        return bd09Encrypt(location.latitude, location.longitude);
    }

    /**
     * @param location 百度地理坐标（BD-09)
     * @return 中国国测局地理坐标（GCJ-02）<火星坐标>
     * @brief 百度地理坐标（BD-09) 转换成 中国国测局地理坐标（GCJ-02）<火星坐标>
     */
    public static LatLng bd09ToGcj02(LatLng location) {
        return bd09Decrypt(location.latitude, location.longitude);
    }

    /**
     * @param location 百度地理坐标（BD-09)
     * @return 世界标准地理坐标（WGS-84）
     * @brief 百度地理坐标（BD-09) 转换成 世界标准地理坐标（WGS-84）
     * <p>
     * ####此接口有1－2米左右的误差，需要精确定位情景慎用
     */
    public static LatLng bd09ToWgs84(LatLng location) {
        LatLng gcj02 = bd09ToGcj02(location);
        return gcj02Decrypt(gcj02.latitude, gcj02.longitude);
    }

    public static class LatLng {
        public double latitude;
        public double longitude;

        public LatLng(double latitude, double longitude) {
            this.latitude = latitude;
            this.longitude = longitude;
        }

        public LatLng() {
        }

        public double getLatitude() {
            return latitude;
        }

        public void setLatitude(double latitude) {
            this.latitude = latitude;
        }

        public double getLongitude() {
            return longitude;
        }

        public void setLongitude(double longitude) {
            this.longitude = longitude;
        }
    }

    /*
     * 大地坐标系资料WGS-84 长半径a=6378137 短半径b=6356752.3142 扁率f=1/298.2572236
     *
     *  根据一点的经纬度和距离来计算另一个点的经纬度
     */
    /**
     * 扁率f=1/298.2572236
     */
    private static double f = 1 / 298.2572236;

    /**
     * 计算另一点经纬度
     *
     * @param lon  wgs84经度
     * @param lat  wgs84维度
     * @param brng 方位角
     * @param dist 距离（米）
     */
    public static LatLng computerThatLonLat(double lon, double lat, double brng, double dist) {

        double alpha1 = rad(brng);
        double sinAlpha1 = Math.sin(alpha1);
        double cosAlpha1 = Math.cos(alpha1);

        double tanU1 = (1 - f) * Math.tan(rad(lat));
        double cosU1 = 1 / Math.sqrt((1 + tanU1 * tanU1));
        double sinU1 = tanU1 * cosU1;
        double sigma1 = Math.atan2(tanU1, cosAlpha1);
        double sinAlpha = cosU1 * sinAlpha1;
        double cosSqAlpha = 1 - sinAlpha * sinAlpha;
        /**
         * 长半径a=6378137
         */
        double longRadius = 6378137;
        /**
         * 短半径b=6356752.3142
         */
        double shortRadius = 6356752.3142;
        double uSq = cosSqAlpha * (longRadius * longRadius - shortRadius * shortRadius) / (shortRadius * shortRadius);
        double A = 1 + uSq / 16384 * (4096 + uSq * (-768 + uSq * (320 - 175 * uSq)));
        double B = uSq / 1024 * (256 + uSq * (-128 + uSq * (74 - 47 * uSq)));

        double cos2SigmaM = 0;
        double sinSigma = 0;
        double cosSigma = 0;
        double sigma = dist / (shortRadius * A), sigmaP = 2 * Math.PI;
        while (Math.abs(sigma - sigmaP) > 1e-12) {
            cos2SigmaM = Math.cos(2 * sigma1 + sigma);
            sinSigma = Math.sin(sigma);
            cosSigma = Math.cos(sigma);
            double deltaSigma = B * sinSigma * (cos2SigmaM + B / 4 * (cosSigma * (-1 + 2 * cos2SigmaM * cos2SigmaM)
                    - B / 6 * cos2SigmaM * (-3 + 4 * sinSigma * sinSigma) * (-3 + 4 * cos2SigmaM * cos2SigmaM)));
            sigmaP = sigma;
            sigma = dist / (shortRadius * A) + deltaSigma;
        }

        double tmp = sinU1 * sinSigma - cosU1 * cosSigma * cosAlpha1;
        double lat2 = Math.atan2(sinU1 * cosSigma + cosU1 * sinSigma * cosAlpha1,
                (1 - f) * Math.sqrt(sinAlpha * sinAlpha + tmp * tmp));
        double lambda = Math.atan2(sinSigma * sinAlpha1, cosU1 * cosSigma - sinU1 * sinSigma * cosAlpha1);
        double C = f / 16 * cosSqAlpha * (4 + f * (4 - 3 * cosSqAlpha));
        double L = lambda - (1 - C) * f * sinAlpha
                * (sigma + C * sinSigma * (cos2SigmaM + C * cosSigma * (-1 + 2 * cos2SigmaM * cos2SigmaM)));

        double revAz = Math.atan2(sinAlpha, -tmp); // final bearing

        System.out.println(revAz);
        System.out.println(lon + deg(L) + "," + deg(lat2));
        LatLng latLng = new LatLng(deg(lat2), lon + deg(L));
        return latLng;
    }

    /**
     * 度换成弧度
     *
     * @param d 度
     * @return 弧度
     */
    private static double rad(double d) {
        return d * Math.PI / 180.0;
    }

    /**
     * 弧度换成度
     *
     * @param x 弧度
     * @return 度
     */
    private static double deg(double x) {
        return x * 180 / Math.PI;
    }
}
```



## 网络请求

+ [Volley](open_code/Volley.md)
+ [Okhttp](open_code/Okhttp.md)
+ [Retrofit](open_code/Retrofit.md)

