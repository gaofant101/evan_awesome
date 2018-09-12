# @`geolocation`

地理位置 `API` 允许用户向 `Web` 应用程序提供他们的位置.
出于隐私考虑,报告地理位置前会先请求用户许可.（部分浏览器需要域名为 `HTTPS` 才能使用这个接口）

## `Api`

`Geolocation` 接口不继承任何方法

`Geolocation.getCurrentPosition()`
确定设备的位置并返回一个携带位置信息的 Position 对象

`Geolocation.watchPosition()`
注册一个位置改变监听器, 每当设备位置改变时, 返回一个 long 类型的该监听器的ID值

`Geolocation.clearWatch()`
取消由 watchPosition()注册的位置监听器

```javascript
function geoFindMe() {
    var output = document.getElementById("out");

    if (!navigator.geolocation) {
        output.innerHTML = "<p>您的浏览器不支持地理位置</p>";
        return;
    }

    function success(position) {
        var latitude = position.coords.latitude;
        var longitude = position.coords.longitude;

        output.innerHTML = '<p>Latitude is ' + latitude + '° <br>Longitude is ' + longitude + '°</p>';

        var img = new Image();
        img.src = "http://maps.googleapis.com/maps/api/staticmap?center=" + latitude + "," + longitude + "&zoom=13&size=300x300&sensor=false";

        output.appendChild(img);
    };

    function error() {
        output.innerHTML = "无法获取您的位置";
    };

    output.innerHTML = "<p>Locating…</p>";

    navigator.geolocation.getCurrentPosition(success, error);
}
```
