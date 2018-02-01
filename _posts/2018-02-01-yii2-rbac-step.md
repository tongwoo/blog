---
layout: post
title: 'Yii2的权限检测流程'
date: 2018-02-01
author: wutong
tags:  php yii
---

Yii2中的`RBAC` 还是比较快捷方便的，支持 PHP、数据库等方式存储权限配置。


### 检查方式

```php
\Yii::$app->authManager->checkAccess(用户id,权限名称,提供给Rule的参数);
//或
\Yii::$app->user->can(权限名称,提供给Rule的参数);
```
返回值为 `bool` 类型，`true` 为有这个权限，`false`为没有这个权限

### checkAccess 检查流程

```php
public function checkAccess($userId, $permissionName, $params = [])
{
    $assignments = $this->getAssignments($userId);
 
    if ($this->hasNoAssignments($assignments)) {
        return false;
    }

    return $this->checkAccessRecursive($userId, $permissionName, $params, $assignments);
}
```
**第一步**，会调用`AuthManager::getAssignments` 方法获得该用户所绑定的角色、权限等信息。

**第二步**，检查此用户的`角色权限是否为空`和`有没有初始化默认角色`，如果都没有的话则返回`false`并终止权限判断。

**第三步**，递归的调用 `AuthManager::checkAccessRecursive` 方法来检查有没有此权限。

### checkAccessRecursive 检查流程

```php
protected function checkAccessRecursive($user, $itemName, $params, $assignments)
{
    if (!isset($this->items[$itemName])) {
        return false;
    }

    /* @var $item Item */
    $item = $this->items[$itemName];
    Yii::trace($item instanceof Role ? "Checking role: $itemName" : "Checking permission : $itemName", __METHOD__);

    if (!$this->executeRule($user, $item, $params)) {
        return false;
    }

    if (isset($assignments[$itemName]) || in_array($itemName, $this->defaultRoles)) {
        return true;
    }

    foreach ($this->children as $parentName => $children) {
        if (isset($children[$itemName]) && $this->checkAccessRecursive($user, $parentName, $params, $assignments)) {
            return true;
        }
    }

    return false;
}
```
**第一步**，判断当前 `AuthManger` 实例中的 `items` 属性中是否存在这个权限，`items` 中保存了所有创建的角色、权限，如果没有的话则直接返回 `false` 并结束。

**第二步**，如果有这个权限的话，则判断这个权限是否绑定了 `Rule` 实例（通过的权限的`ruleName`属性值是否为`null`来判断），如果绑定了`Rule`则执行`Rule`实例的`execute`方法，然后根据`execute`方法的返回值觉得是否终止检查。

**第三步**，判断用户的当前的`$assignments`中是否存在这个权限 或者 当前默认所有角色中是否存在这个权限，满足其中一种的话则返回`true`,注意：如果权限实际是角色的话才有意义，因为判断代码为 `in_array($itemName, $this->defaultRoles)`

**第四步**，循环检查`AuthManager::children`属性里面每个项的`value`数组中是否包含了要验证的权限并且递归调用`checkAccessRecursive`检查当前用户是否有这个项的`key`对应的权限，如两者都满足的话则返回`true`并终止判断。








