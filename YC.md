---


---

<h3 id="单场胜负与单场玩法间的联动关系未实现">1.单场胜负与单场玩法间的联动关系未实现</h3>
<blockquote>
<p>联动系数：单局玩法主队胜率 =（主队胜率-0.5)*单玩法联动参数+0.5</p>
</blockquote>
<h4 id="修正记录">修正记录</h4>
<p><img src="https://lh5.googleusercontent.com/hpJXZK0whyygkxbSQYZCBDpHixtdfhBpudMuqHxDXRaX_SkSa4CrZfa0R9i_WJitcOYxNu2euUOuGKpVomlTIVI7KXei-RGMdhz5OqrdEhTuPHj3VNoqPL75DJRb0ne2POYf9nVK" alt=""></p>
<p>开启了单场胜者联动的玩法，会出现联动系数配置框。</p>
<p>反向计算公式：<br>
单局玩法主队胜率 - 0.5 = （主队胜率-0.5)*单玩法联动参数<br>
(单局玩法主队胜率 - 0.5)/单玩法联动参数 = 主队胜率-0.5<br>
单玩法联动参数 = (单局玩法主队胜率 - 0.5) / 主队胜率-0.5</p>
<hr>
<h3 id="让分盘更改盘口数量后只能增加盘口数量不能减少。">2.让分盘更改盘口数量后只能增加盘口数量不能减少。</h3>
<h4 id="修正记录-1">修正记录</h4>
<p><img src="https://lh3.googleusercontent.com/_wqD2ZjeP2dzsgqNdgH189Qzubnv3eTl4H-Xx9buqdFS0aI9dC6fhxFsoreF7h0pzHBEFkf1wC3W1klTXAWLdaJZ1MfsmY15prD2oesatlpA0VEOiPzHz2cBR-1VG4wOU2EjXorF" alt=""><br>
更改数量之后<br>
<img src="https://lh5.googleusercontent.com/Lc55CFkg0ogoXL2ZBzGJLppgPuYTcRofDBIV2-qg--V1rNf3msVyG9z58L_eao5XQFHPCs5zF-9CRkrnt9oLEzsHp3dJUf74hQVls3eINim5dYhI1yt5LcOh6XUTWzpD5ukdnpI4" alt=""></p>
<hr>
<h3 id="盘口模板导入后">3.盘口模板导入后</h3>
<blockquote>
<p>赔率不能导入、标题类盘口不能导入、盘口配置属性不能导入，导入后的大小，让分盘的组数跟设置中的组数不同，盘口模板导入的赛事无法领盘口，有几率无法审核导入的盘口</p>
</blockquote>
<h4 id="bug重现">BUG重现</h4>
<blockquote>
<p>导入模板之后，胜负盘口的赔率正常，有参数设定的盘口均不正常。</p>
</blockquote>
<ol>
<li>排查：导入之后的参数设定字段<br>
Title 类型的盘口参数未正确导入<br>
检查模板：</li>
</ol>
<p><code>{ 	"Template":{"Rebate":0.935,"Auto":0.5,"Jump":1,"Limit":1}, 	"Flag":1, 	"Bets":{ 		"Winner":{ 			"PlayCode":"Winner", 			"Items":[			{"Group":0.0000,"Index":0,"Odds":null,"WinRate":0.474809483264},{"Group":0.0000,"Index":1,"Odds":null,"WinRate":0.525190516736} 			], 			"Template":{"Rebate":0.935,"Auto":0.5,"Jump":1,"Limit":1}, 			"Setting":"", 			"Header":{"Items": 				[ 				{"Type":2,"Key":""},"Type":3,"Key":""} 				]}, 			"Flag":0, 			"Maps":null, 			"Group":"" 		}... 	} }</code><br>
模板中Setting数据正确<br>
2.  原因：未正确刷新到缓存引起<br>
<strong>注意：全场玩法不会从模板中加载赔率（全场的赔率来自于单场胜者的赔率联动），此问题不是BUG</strong></p>
<hr>
<h3 id="、复制盘口">4、复制盘口</h3>
<blockquote>
<p>组合类型的盘口无法复制到其他局，盘口的显示锁定属性无法复制到其它局，选项的锁定和隐藏属性也无法复制到其它局</p>
</blockquote>
<h4 id="bug重现-1">BUG重现</h4>
<ol>
<li>赔率复制 ： <strong>正常</strong></li>
<li>盘口锁定状态复制：<strong>异常</strong><br>
2.1  因缓存未写入引起，已修正。</li>
<li>修改盘口参数设定之后的复制<br>
3.1. 标题类复制测试通过</li>
</ol>
<hr>
<h3 id="、修改返奖、限红、跳水，页面数据不实时刷新。批量修改返奖、限红、跳水功能无效">5、修改返奖、限红、跳水，页面数据不实时刷新。批量修改返奖、限红、跳水功能无效</h3>
<h3 id="bug重现-2">BUG重现</h3>
<ol>
<li>修改单个盘口的限红、跳水，页面可自动更新</li>
<li>修改返奖率，赔率不会联动更新<br>
2.1 前端脚本问题 ，已修正，返奖率修改会联动赔率一起变动.</li>
<li>批量修改返奖 修正成功。</li>
<li>批量修改跳水方案，修正成功</li>
<li>批量修改限红方案，修正成功</li>
</ol>
<hr>
<h3 id="、赛事直播中添加遮罩无效">6、赛事直播中添加遮罩无效</h3>
<hr>
<h3 id="、大小盘、让分盘中修改联动参数不实时更新赔率。">7、大小盘、让分盘中修改联动参数不实时更新赔率。</h3>
<p>联动已实现，修改联动参数以及增加数量，赔率会自动填上。</p>
<hr>
<h3 id="、标签页面-无法进行排序操作">8、标签页面 无法进行排序操作</h3>
<hr>
<h3 id="、战队类型的盘口无法自动引入战队">9、战队类型的盘口无法自动引入战队</h3>
<hr>
<h3 id="、审核通过的赛事需要再次刷新缓存才在前台显示">10、审核通过的赛事需要再次刷新缓存才在前台显示</h3>
<hr>
<h3 id="、赔率低于1盘口需要自动锁定">11、赔率低于1盘口需要自动锁定</h3>
<blockquote>
<p>赔率小于1由前端进行判断，在前端的显示效果为锁定</p>
</blockquote>
<hr>
<h3 id="、自动切换大小和让分的功能未实现">12、自动切换大小和让分的功能未实现</h3>
<hr>
<h3 id="、选项太多的玩法在管理页面无法操作后面的选项内容">13、选项太多的玩法在管理页面无法操作后面的选项内容</h3>
<blockquote>
<p>已解决。 layui-table 上增加样式标记：break-all</p>
</blockquote>
<hr>
<h3 id="、赔率设置不正确的盘口不能审核">14、赔率设置不正确的盘口不能审核</h3>
<blockquote>
<p>测试未设置赔率的盘口，不可以通过审核。</p>
</blockquote>
<hr>
<h3 id="、滚球如果比赛开始无人接盘，赛事需要变为锁定状态，后台提醒操盘进行处理">15、滚球如果比赛开始无人接盘，赛事需要变为锁定状态，后台提醒操盘进行处理</h3>
<hr>
<h3 id="、在赛事管理页面有未审核的赛事可以更改标题和赛制">16、在赛事管理页面有未审核的赛事可以更改标题和赛制</h3>
<blockquote>
<p>未审核的赛事如果赛制建错，只可删除重建。如果更改的话，涉及到联动数据过多。</p>
</blockquote>
<hr>
<h3 id="、自由选项盘口，如果新增的选项被删除在盘口页面还是会显示一个空的栏目">17、自由选项盘口，如果新增的选项被删除在盘口页面还是会显示一个空的栏目</h3>
<blockquote>
<p>已修正</p>
</blockquote>
<hr>
<h3 id="、bo3-全场让分少了一组-1.5的盘口">18、bo3 全场让分少了一组 +1.5的盘口</h3>

