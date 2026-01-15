source/module/forum/forum_tag.php

1.        $recent_use_tag = array();
2.        $i = 0;
3.        $query = C::t('common_tagitem')->select(0, 0, 'tid', 'itemid', 'DESC', 10);
4.        foreach($query as $result) {
5.             ///[UPGRADE#取消最近使用tag数量限制为4，默认为10]
6. //        if($i > 4) {
7. //           break;
8. //        }