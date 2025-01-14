---
title: 日志转发
intro: '{% data variables.product.product_name %} 使用 `syslog-ng` 将 {% ifversion ghes %}system{% elsif ghae %}Git{% endif %} 和应用程序日志转发到你指定的服务器。'
redirect_from:
  - /enterprise/admin/articles/log-forwarding
  - /enterprise/admin/installation/log-forwarding
  - /enterprise/admin/enterprise-management/log-forwarding
  - /admin/enterprise-management/log-forwarding
  - /admin/user-management/log-forwarding
  - /admin/user-management/monitoring-activity-in-your-enterprise/log-forwarding
versions:
  ghes: '*'
  ghae: '*'
type: how_to
topics:
  - Auditing
  - Enterprise
  - Logging
  - Security
ms.openlocfilehash: 935c8f0221c4541d2801a5e705779efff3d34370
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2022
ms.locfileid: '145098697'
---
## 关于日志转发

支持 syslog 样式日志流的任何日志收集系统都受支持（例如 [Logstash](http://logstash.net/) 和 [Splunk](http://docs.splunk.com/Documentation/Splunk/latest/Data/Monitornetworkports)）。

启用日志转发时，必须上传 CA 证书以加密 syslog 端点之间的通信。 您的设备和远程 syslog 服务器将执行双向 SSL，每个服务器向另一个服务器提供证书并验证收到的证书。

## 启用日志转发

{% ifversion ghes %}
1. 在 {% data variables.enterprise.management_console %} 设置页面的左侧边栏中，单击“监视”。
1. 选择“启用日志转发”。
1. 在“服务器地址”字段中，输入要将日志转发到的服务器的地址。 您可以在以逗号分隔的列表中指定多个地址。
1. 在 Protocol 下拉菜单中，选择用于与日志服务器通信的协议。 该协议将应用到所有指定的日志目标。
1. （可选）选择“启用 TLS”。 我们建议根据本地安全策略启用 TLS，尤其是在设备和任何远程日志服务器之间存在不受信任的网络时。 
1. 要加密 syslog 终结点之间的通信，请单击“选择文件”，然后为远程 syslog 服务器选择 CA 证书。 您应上传 CA 捆绑包，其中包含对远程日志服务器的证书进行签名所涉及的 CA 的证书串联。 将对整个证书链进行验证，且证书链必须以根证书结束。 有关详细信息，请参阅 [syslog-ng 文档中的 TLS 选项](https://support.oneidentity.com/technical-documents/syslog-ng-open-source-edition/3.16/administration-guide/56#TOPIC-956599)。
{% elsif ghae %} {% data reusables.enterprise-accounts.access-enterprise %} {% data reusables.enterprise-accounts.settings-tab %}
1. 在 {% octicon "gear" aria-label="The Settings gear" %}“设置”下，单击“日志转发” 。
  ![日志转发选项卡](/assets/images/enterprise/business-accounts/log-forwarding-tab.png)
1. 在“日志转发”下，选择“启用日志转发”。
  ![启用日志转发的复选框](/assets/images/enterprise/business-accounts/enable-log-forwarding-checkbox.png)
1. 在“Server address（服务器地址）”下，输入您想要日志转发到的服务器地址。
  ![服务器地址字段](/assets/images/enterprise/business-accounts/server-address-field.png)
1. 使用“Protocol（协议）”下拉菜单选择一个协议。
  ![协议下拉菜单](/assets/images/enterprise/business-accounts/protocol-drop-down-menu.png)
1. （可选）要在 syslog 终结点之间启用 TLS 加密通信，请选择“启用 TLS”。
  ![启用 TLS 的复选框](/assets/images/enterprise/business-accounts/enable-tls-checkbox.png)
1. 在“Public certificate（公共证书）”下，粘贴您的 x509 证书。
  ![公共证书的文本框](/assets/images/enterprise/business-accounts/public-certificate-text-box.png)
1. 单击“ **保存**”。
  ![用于日志转发的保存按钮](/assets/images/enterprise/business-accounts/save-button-log-forwarding.png) {% endif %}

{% ifversion ghes %}
## 故障排除

如果遇到日志转发方面的问题，请联系 {% data variables.contact.contact_ent_support %} 并在电子邮件中附上 `http(s)://[hostname]/setup/diagnostics` 的输出文件。
{% endif %}
