---

subtitle:    "TCP/IP illustrated"
author:      "Steven"
description: "TCP/IP"
header-mask: 0.5
catalog: ture
multilingual: true
header-img:  "img/home-bg.jpg"
tags:
    - TCPIP

---


<!-- Chinese Version -->
<div class="zh post-container">
    {% capture about_zh %}
        {% include post/tcpipillustrated/chapter01.md %}
    {% endcapture %}
    {{ about_zh | markdownify }}
</div>

<!-- English Version -->
<div class="en post-container">
    {% capture about_en %}
        {% include post/tcpipillustrated/chapter01.md %}
    {% endcapture %}
    {{ about_en | markdownify }}
</div>
