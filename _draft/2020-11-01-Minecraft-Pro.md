---

subtitle:    "Welcome to Minecraft Pro"
author:      "Salious"
description: "This is how to install and play minecraft pro game"
header-mask: 0.5
catalog: ture
multilingual: true
header-img:  "img/home-bg.jpg"
tags:
    - minecraft

---


<!-- Chinese Version -->
<div class="zh post-container">
    {% capture about_zh %}
        {% include post/minecraft/minecraftpro.md %}
    {% endcapture %}
    {{ about_zh | markdownify }}
</div>

<!-- English Version -->
<div class="en post-container">
    {% capture about_en %}
        {% include post/minecraft/minecraftpro.md %}
    {% endcapture %}
    {{ about_en | markdownify }}
</div>
