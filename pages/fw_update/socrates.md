---
sidebar: home_sidebar
title: Update firmware on socrates
folder: fw_update
permalink: /devices/socrates/fw_update/
device: socrates
---
{% assign device = site.data.devices[page.device] %}
{% capture path %}templates/device_specific/{{ device.firmware_update }}.md{% endcapture %}
{% include {{ path }} %}
