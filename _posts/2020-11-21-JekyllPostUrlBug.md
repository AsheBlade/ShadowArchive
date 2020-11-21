---
layout: post
title: Jekyll Post_url Bug
date: 2020-11-21
author: Shadow Walker
tags: [Bug]
toc: true
comments: true
---

今天发生了一个很有意思的bug,  就是关于Internal Link
```
// The stuff afer post_url is basically the md file name. 
{% raw %}
[Name of Link]({% post_url 2020-08-25-Java_Syntax %})
[]({% post_url  %})
{% endraw %}
```

突然发现之前所有的internal link都不能正常打开了, 全是404. 

于是, 我看了一下Local环境, 都没问题啊. 问题在哪里呢? 

1. 我去查了Jekyll 的官方文档, 又测试了几次, 发现miss掉了baseurl, 于是我去查config, 发现也没问题呀
2. 我去Google, Stack Overflow告诉我要升级Jekyll到4.0. 我在local升级, 结果还是local没问题, github-page部署之后就出问题. 
3. 我去看Github官方的文档, 看了半天, 得出结论还是一样, 我不可能去升级github内部的jekyll版本. 
4. 最后我看到了这个: 

![](https://lh3.googleusercontent.com/opepmk8sMzjE2JHy9EnF2n87djdBca-CXq36_vnRDufGutb28zHMZi7Fekk1GP0-qli9nuRZGlj9j4lgaXoSZJZYxdib6ItOGI1Iweo9szXNTWKCcX0pLcMRPvr0QqTOodWJE1keSLX18TEaqgayu_hoOodE7otgOUpzou3ZEC9iJvS3nyDyU2VOOmMQvSLEA4WoOorNyuzyZDdwmHW6sUxP1dqu_dxds5OcsWnBY5H0tJVzf4FwDfSI5niue0bFCyFqICZKj5NH-mQoNQPqyCduxvk5VM6U-0auTtdFxojT9Ew51ytdIfAI497dlUePl5e5i_ljMA4TJA8V3p_6FZKWKhrQcz-_6UO8zwEA4azP97CsPtjtmXwDN4xyIl1VueaTKN60YmPORlUZR5BC-kZf9r6Xt0TOuT-18b9C49d1eRSdW-HMEWkTcPt65qPaSBjAC8I44MMBwMg1sylk-24KFtJ6OMJyZyQHjBq9i4Cm18YvvVIP7kIQn8FakJmguD6IEd0bAE2sNewuYTMRDhMZpHk70Ez6jDZ4mjfcsB6nrVOOpN299J6hZiVAFga4oetZcCjlnn1Nw99O4HDEEb9cF59VA2TmaVUOP3OmKIz1hjsWLL9npRKE96JECu6YEV-nZVci0if_xNBtmKOg7p0gahhNTQ2ntwElOUMMdqmXeZx4FhyKDeVuM4xr1A=w621-h360-no?authuser=0)

![](https://lh3.googleusercontent.com/o9iuFfx5Z8qMD4EKQdiVnnSwaL2XreA7GHCJJOcLditZHH8uxYrVkLX8-F695z8zSeR--ygBPJyCbr2qe8-qNQ5Y0nB3HtKMFeAJOgXVfFYfC91sRG17u8zCr2Be1M3uOx2U3Q4m_a_6MHMNUP3P6m2wg5mrlJ3BTeKuq9t429DUUjEhY9ejKp-Vl94GvgBE56hjajKqhT4DgJgJAZMoHGI_HZLxG6aXcNH2unphnmtoKi-6ro1zvJz8mH0GVE699bwNb8ODzDnLFiNvAumsMzMnPEv3R--9TCYqlFV8f3mmkltkLFUdRBDQt9hzUhIhqNhrDb3FsGt_Z-7mMSjScRnqY0ARZ9AUJxaQjr1J4vitUfe_c4hSL_HMtVeXlgsuQv72ifKUa9o71TeDMd5VTHdwr8swUv7II--8svLncKQYufBMY7Guon9AuBe8cvsb_35oBP0SO21Gn6R_YOSV-OolfNjMT4iiKzbD13s0Q3WNLWagYQlfvtqLp7mHbYXIaFAY3hJLqe4GcpcP41PQueqL3wixDUP7gv8HGOT1pSEfoQVxaV2Y5BLg6ErYNIdKpIcz6qAJGIo9wWixqUtEbuvN3_St3m50YGA2-2Zb9HJdQNJ5AuV6VOQKx3mEP-7ARwmlFFC5yc9SJVsx2O0rpJMh61Jv9cbttpwy0oAtpcDYShl9gj7dcDfSxoHRmg=w912-h455-no?authuser=0)

瞬间气乐了, Jekyll在一年前就公布了4.0, 但Github现在还在用3.9, 难怪我在Local测试没问题, 一deploy到github 就出错. 

一个可行的解决办法, 就是用旧的syntax, 在前面加site.baseurl, 不过这个办法其实没法根本上解决. 

**因为经过local测试, 新的4.0不接受这个旧的syntax, 但3.9不接受新的syntax**

也就是说, 如果改过来之后以后github更新了4.0, 这些就都用不了了.  所以, 也就只能先这么放着了. 长远看, 这么写还是好的, Github以后肯定还是会更新的.  现在于是只能用local部署去看文档, 以解决link失效的问题

```
{% raw %}
[xyx]({{site.baseurl}}{%link _posts/2020-11-06-UphillDownhill.md %})
{% endraw %}
```

这个故事告诉我们: 

**Production 和 development的环境一致是多么重要啊!**

