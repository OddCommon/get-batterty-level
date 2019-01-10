
###  [ `Return | 首页` ](https://github.com/PicoSupport/PicoSupport)
* [AndroidDemo | 安卓](https://github.com/PicoSupport/PicoSupport/blob/master/android.md)
* [UnityDemo | Unity3d](https://github.com/PicoSupport/PicoSupport/blob/master/unity.md)

## Unity_Demo_BatteryManager

## Unity_Versions：
- 2017.1.0f3 Or UP

## Explain 说明：

- 功能：访问pico设备当前电量

Demo主要C#代码 BatteryManager.cs文件

```C#
public class BatteryManager : MonoBehaviour {

    public Text Power;
    string _time = string.Empty;
    string _battery = string.Empty;
	void Start () {
        StartCoroutine("UpdataBattery");
	}
    void Update()
    {

    }
    IEnumerator UpdataBattery()
    {
        while (true)
        {
            _battery = GetBatteryLevel().ToString();
            Power.text = "Battery "+_battery + "%";
            yield return new WaitForSeconds(120f);
        }
    }
    int GetBatteryLevel()
    {
        try
        {
            string CapacityString = System.IO.File.ReadAllText("/sys/class/power_supply/battery/capacity");
            return int.Parse(CapacityString);
        }
        catch (Exception e)
        {
            Debug.Log("Failed to read battery power; " + e.Message);
        }
        return -1;
    }
}
```

## Use 使用：
- 场景位置： Assets -> Scenes -> ShowBatteryLevel
- 打包Apk文件，在pico设备打开，能够看到设备当前电量

## Announcements 注意事项：
- 本demo不能再Pc端测试

## Pico技术支持
欢迎更多地了解我们，如果您有任何问题，请联系我们。
Learn about us, and contact us if you have any questions. 

- Email:  support@picovr.com
- Web:  [https://www.picovr.com/](https://www.picovr.com/)
