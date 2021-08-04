---

subtitle:    "Binary tree"
author:      "wangzhui"
description: "Binary tree creat and print"
header-mask: 0.5
catalog: ture
multilingual: true
header-img:  "img/home-bg.jpg"
tags:
    - Ruby
    - Jekyll

---

<!-- Chinese Version -->
<div class="zh post-container">
    {% capture about_zh %}
        {% include post/tree.md %}
    {% endcapture %}
    {{ about_zh | markdownify }}
</div>

<!-- English Version -->
<div class="en post-container">
    {% capture about_en %}
        {% include post/tree.md %}
    {% endcapture %}
    {{ about_en | markdownify }}
</div>

