---
layout: post
title:  "Dream Team Machine"
date:   2016-08-15 11:55:14 +0300
categories:

info: Here we want to share the experience we gained and challenges we faced when creating the machine for deep learning tasks.
---
After taking the second place in [BlackBox Challenge][bb], we decided to invest the money won in new hardware so as to enhance our computing facilities in forthcoming competitions related to Deep Reinforcement Learning. There are several good publications explaining how to build a good Deep Learning Machine, for example, [Tim Dettmers][tim] from March 2015, [Roelof Pieters][roelof] from September 2015, [Petteri Teikari][teikari] from August 2016. In this post, we are going to share with readers the experience we gained and challenges we faced with when creating our own Dream Team Machine.

![Dream Team Machine](/assets/DTM.gif){:class="center-image"}

With an intension to save time and money, we took advantage of the services offered by one of the most cheapest and trusted online hardware stores, [regard.ru][regard]. The shop has a variety of goods; however, our budget was limited to $2500. Here is the final list of our purchase:

<b>Chassis:</b> Corsair Carbide Series Air 240 ($103) - that was our main mistake. We wanted to have a compact machine, but it turned out that such compactness had more shortcomings than we expected. First, we were forced to limit the motherboard form factor to mATX. Second, (most important) it was not compatible with our GPU choice, GTX1080 Palit. Fortunately, we were able to find a simple and convenient alternative - Cooler Master Elite 335U.

<b>Motherboard:</b> ASUS X99-M WS ($252) - the cheapest card available at regard.ru, with mATX form factor, full support of all Intel LGA2011-v3 processors, and built-in WiFi, which (by the way) was useless for our purposes. The most important drawback of the motherboard was its lack of support for Linux. For example, lm_sensors are [not working][nct] properly with NCT6791D chip.

<b>CPU:</b> Intel Core i7-5820K ($408) - the cheapest Intel LGA2011-v3 processor in the store. It has 6 cores that greatly assist in the development of multi-threaded algorithms for reinforcement learning tasks.

<b>CPU cooler:</b> Noctua NH-L9x65 ($55) - low-profile cooler with 65mm height. The choice was mainly affected by the restriction on CPU cooler's maximum height: no more than 120mm for Air 240.

<b>SSD:</b> 512Gb SSD Samsung 950 Pro Series ($352) - the device was new for us, but we decided that accelerating the read/write speed worth spending a bit more money.

<b>Memory:</b> 32Gb DDR4 2666MHz Kingston HyperX Savage 2x16Gb KIT ($196) - there are two free slots that can be used for upgrades.

<b>Power supply:</b> 1000W Corsair RM1000x ($201) - taking into account the possibility of purchasing the second GPU card, this gold-certified device was a great choice.

<b>GPU:</b> nVidia GeForce GTX1080 Palit GameRock Premium PCI-E 8192Mb ($775) - with the board size of 285 x 133 x 45, it could hardly fit into Air 240 (only if one first inserts it into the motherboard and then into chassis). Moreover, we totally forgot about the power connection located on the top of the card. It also occupied two PCIe slots (photo below).

Fortunately, we managed to pick up all the purchased items in Moscow.

<table>
<tr>
<td>{% include picture.html name="IMG_0695" alt="Corsair Air 240 is not compatible with GTX1080 Palit" group="1" %}</td>
<td>{% include picture.html name="IMG_0730" alt="GTX1080 Palit takes two PCIe slots" group="1" %}</td>
<td>{% include picture.html name="IMG_0732" alt="We bought an additional cooler for PC case" group="1" %}</td>
<td>{% include picture.html name="IMG_0736" alt="Machine is well placed in the server rack" group="1" %}</td>
</tr>
</table>

<br />

Final remarks and tips:
<ul>
    <li>
		Check twice the size of components, especially that of GPU cards, which can occupy up to three slots or be higher due to power supply wires.
    </li>
    <li>
		The latest ASUS desktop motherboards are not Linux friendly, and you may not be able to monitor such critical PC parameters as power supply voltages, fan speeds and temperatures.
    </li>
</ul>

We would like to thank the [Department of Secure Information Technology][cit] at ITMO University for providing us with a simple but useful PC case and with a place in a server rack.


[bb]: http://blackboxchallenge.com/home/
[tim]: http://timdettmers.com/2015/03/09/deep-learning-hardware-guide/
[roelof]: http://graphific.github.io/posts/building-a-deep-learning-dream-machine/
[teikari]: http://www.slideshare.net/PetteriTeikariPhD/deep-learning-workstation
[regard]: http://www.regard.ru
[nct]: https://github.com/groeck/nct6775/issues/30
[cit]: https://cit.ifmo.ru
