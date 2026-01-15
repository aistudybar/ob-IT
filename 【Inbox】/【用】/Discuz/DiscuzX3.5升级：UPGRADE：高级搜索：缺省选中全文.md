template\default\search\forum_adv.htm：  
找到：  
<input type="checkbox" name="srchtype" class="pc" value="fulltext" {$fulltextchecked}{if $posttableselect}">  
  
替换为：  
<input type="checkbox" name="srchtype" class="pc" value="fulltext" {eval echo isset($fulltextchecked) ? $fulltextchecked : 'checked'}{if $posttableselect} onclick="