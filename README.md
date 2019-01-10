<p align="right"><a href="https://github.com/PicoSupport/PicoSupport" target="_blank">Pico Support Home</a></p>

## Unity_Demo_BatteryManager

## Unity Versions：
- 2017.1.0f3 and later

## Description：

- Access the current power of pico device

Demo Main code **BatteryManager.cs**

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

## Usage：
- Scene： Assets -> Scenes -> ShowBatteryLevel
- Pack the Apk file, open it in the pico device, and you can see the current power of the device

## Announcements：
- This demo cannot be tested on Pc

