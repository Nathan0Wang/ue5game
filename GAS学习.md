# GAS学习

![image-20240614221616194](G:\ue5game\Aura\Figure\image-20240614221616194.png)

![image-20240614224349620](G:\ue5game\Aura\Figure\image-20240614224349620.png)

![image-20240615093254924](G:\ue5game\Aura\Figure\image-20240615093254924.png)

Mixed更新GameplayEffects到Player，多用于Player，Minimal不更新，多用于AI。

![image-20240615094515519](G:\ue5game\Aura\Figure\image-20240615094515519.png)

对于enemy ownerActor和AvatarActor是一致的，对于player来说，由于AbilitySystemComponent在PlayerState中，所以OwnerActor在PlayerState中，AvatarActor在Player中。

![image-20240615095607080](G:\ue5game\Aura\Figure\image-20240615095607080.png)

OnRep为Replicate的回调函数，服务器在复制后通知Client会调用OnRep。

![image-20240615102205850](G:\ue5game\Aura\Figure\image-20240615102205850.png)

![image-20240615102813025](G:\ue5game\Aura\Figure\image-20240615102813025.png)

Prediction可以允许Client先修改数值，避免网络延迟，服务器判断是否有效，如果无效Server会回滚Client数值。

```c++
GAMEPLAYATTRIBUTE_REPNOTIFY(UAuraAttributeSet, Health, OldHealth);
```

用于Prediction

```cpp
DOREPLIFETIME_CONDITION_NOTIFY(UAuraAttributeSet, Health, COND_None, REPNOTIFY_Always);
```

COND_None 无条件复制

REPNOTIFY_Always 总是通知，REPNOTIFY_OnChanged 改变值时通知