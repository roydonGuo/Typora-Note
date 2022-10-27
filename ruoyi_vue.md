

# ruoyi_vue







## 遍历封装多级部门



```java
/**
 * 递归列表
 */
private void recursionFn(List<SysDept> list, SysDept t) {
    // 得到子节点列表
    List<SysDept> childList = getChildList(list, t);
    t.setChildren(childList);
    for (SysDept tChild : childList) {
        if (hasChild(list, tChild)) {
            recursionFn(list, tChild);
        }
    }
}

/**
 * 得到子节点列表
 */
private List<SysDept> getChildList(List<SysDept> list, SysDept t) {
    List<SysDept> tlist = new ArrayList<SysDept>();
    Iterator<SysDept> it = list.iterator();
    while (it.hasNext()) {
        SysDept n = (SysDept) it.next();
        if (StringUtils.isNotNull(n.getParentId()) && n.getParentId().longValue() == t.getDeptId().longValue()) {
            tlist.add(n);
        }
    }
    return tlist;
}

/**
 * 判断是否有子节点
 */
private boolean hasChild(List<SysDept> list, SysDept t) {
    return getChildList(list, t).size() > 0;
}
```



楠哥p11





