# AWS Shield Advanced quotas<a name="shield-limits"></a>

AWS Shield Advanced has default quotas on the number of entities per Region\. You can [request an increase](https://console.aws.amazon.com/servicequotas/home/services/shield/quotas) in these quotas\.


| Resource | Default quota | 
| --- | --- | 
|  Maximum number of protected resources for each resource type that AWS Shield Advanced offers protection for, per account\.   |  1,000  | 
|  Maximum number of protection groups, per account\.   |  100  | 
|  Maximum number of individual protected resources that you can specifically include in a protection group\. In the API, this applies to the `Members` that you specify when you set the protection group `Pattern` to `ARBITRARY`\. In the console, this applies to the resources that you select for the protection grouping **Choose from protected resources**\.  |  1,000  | 