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

![image-20240615152401012](G:\ue5game\Aura\Figure\image-20240615152401012.png)



## Gamplay Effects

创建widgetController负责widget和model之间的数据交互

![image-20240616102312512](G:\ue5game\Aura\Figure\image-20240616102312512.png)

3种改变属性的方式

![image-20240616102624287](G:\ue5game\Aura\Figure\image-20240616102624287.png)

![image-20240616154257484](G:\ue5game\Aura\Figure\image-20240616154257484.png)

Instant&Periodic永久改变属性

![image-20240616161138849](G:\ue5game\Aura\Figure\image-20240616161138849.png)

Stacking -Aggregate by Source

​		-Aggregate by Target

OverlayWidgetController 查找DT

![image-20240621190814913](G:\ue5game\Aura\Figure\image-20240621190814913.png)

多Modifier计算顺序

![image-20240621191052179](G:\ue5game\Aura\Figure\image-20240621191052179.png)

Modifier计算顺序

![image-20240621192428962](G:\ue5game\Aura\Figure\image-20240621192428962.png)

增加属性步骤

![image-20240621192505720](G:\ue5game\Aura\Figure\image-20240621192505720.png)

属性关系

![image-20240622091042387](G:\ue5game\Aura\Figure\image-20240622091042387.png)

**Draw As Border**

![image-20240622104229418](G:\ue5game\Aura\Figure\image-20240622104229418.png)

当属性菜单关闭时CallAttributeMenuClosed，Overlay就能知道属性菜单关闭恢复菜单按钮

![image-20240622110036305](G:\ue5game\Aura\Figure\image-20240622110036305.png)

属性菜单更新流程

![image-20240622153855000](G:\ue5game\Aura\Figure\image-20240622153855000.png)

```c++
template<class T>
using TStaticFuncPtr = typename TBaseStaticDelegateInstance<T, FDefaultDelegateUserPolicy>::FFuncPtr;
```

```c++
TStaticFuncPtr<float(int32, float, int32)> RandomFuncPtr;
// equal to
static float RandomFunc(int32 x, float y, int32 z) {return y;}
```

可以存储函数，执行是这样的

```c++
float res = RandomFuncPtr(0, 0.f, 0);
```