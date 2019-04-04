---
title: PowerIrpDDIs ルール (wdm)
description: PowerIrpDDIs ルールを指定するシステムまたは IRP のデバイス ドライバーが処理するときに\_MJ\_IRP で電源\_MN\_設定\_電源に呼び出す必要はありませんパッシブでの呼び出しは、必ずDdi\_レベル。
ms.assetid: C56C73E5-75D6-427A-8582-24D6B1404A70
ms.date: 05/21/2018
keywords:
- PowerIrpDDIs ルール (wdm)
topic_type:
- apiref
api_name:
- PowerIrpDDIs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e1381ccd17ca37053491a16b97b4f8aad1f20887
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536844"
---
# <a name="powerirpddis-rule-wdm"></a>PowerIrpDDIs ルール (wdm)


**PowerIrpDDIs**ルールを指定する、システムまたは IRP のデバイス ドライバーが処理するときに\_MJ\_IRP で電源\_MN\_設定\_電源に呼び出す必要はありません Ddiパッシブで通話できるだけ\_レベル。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PowerIrpDDIs</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**ExIsProcessorFeaturePresent**](https://msdn.microsoft.com/library/windows/hardware/ff545442)
[**ExRaiseAccessViolation**](https://msdn.microsoft.com/library/windows/hardware/ff545509)
[**ExRaiseDatatypeMisalignment**](https://msdn.microsoft.com/library/windows/hardware/ff545524)
[**ExUuidCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545658)
[**HalExamineMBR**](https://msdn.microsoft.com/library/windows/hardware/ff546584)
[**HalGetInterruptVector**](https://msdn.microsoft.com/library/windows/hardware/ff546612)
[**IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)
[**IoBuildSynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548330)
[**IoCheckShareAccess**](https://msdn.microsoft.com/library/windows/hardware/ff548341)
[**IoConnectInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff548371)
[**IoCreateController**](https://msdn.microsoft.com/library/windows/hardware/ff548395)
[**IoCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff548418)
[**IoCreateSymbolicLink**](https://msdn.microsoft.com/library/windows/hardware/ff549043)
[**IoCreateSynchronizationEvent**](https://msdn.microsoft.com/library/windows/hardware/ff549045)
[**IoCreateUnprotectedSymbolicLink**](https://msdn.microsoft.com/library/windows/hardware/ff549050)
[**IoDeleteController**](https://msdn.microsoft.com/library/windows/hardware/ff549078)
[**IoDeleteSymbolicLink**](https://msdn.microsoft.com/library/windows/hardware/ff549085)
[**IoDetachDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549087)
[**IoDisconnectInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff549089)
[**IoGetConfigurationInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549157)
[**IoGetDeviceInterfaceAlias**](https://msdn.microsoft.com/library/windows/hardware/ff549180)
[**IoGetDeviceInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff549186)
[**IoGetDeviceNumaNode**](https://msdn.microsoft.com/library/windows/hardware/ff549191)
[**IoGetDeviceObjectPointer**](https://msdn.microsoft.com/library/windows/hardware/ff549198)
[**IoGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff549203)
[**IoGetDevicePropertyData**](https://msdn.microsoft.com/library/windows/hardware/ff549206)
[**IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)
[**IoGetFileObjectGenericMapping**](https://msdn.microsoft.com/library/windows/hardware/ff549231)
[**IoInitializeTimer**](https://msdn.microsoft.com/library/windows/hardware/ff549344)
[**IoIsWdmVersionAvailable**](https://msdn.microsoft.com/library/windows/hardware/ff549382)
[**IoOpenDeviceInterfaceRegistryKey**](https://msdn.microsoft.com/library/windows/hardware/ff549433)
[**IoOpenDeviceRegistryKey**](https://msdn.microsoft.com/library/windows/hardware/ff549443)
[**IoRegisterBootDriverReinitialization**](https://msdn.microsoft.com/library/windows/hardware/ff549494)
[**IoRegisterDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff549506)
[**IoRegisterDriverReinitialization**](https://msdn.microsoft.com/library/windows/hardware/ff549511)
[**IoRegisterLastChanceShutdownNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549518)
[**IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)
[**IoRegisterShutdownNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549541)
[**IoRemoveShareAccess**](https://msdn.microsoft.com/library/windows/hardware/ff549587)
[**IoReportDetectedDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549597)
[**IoReportTargetDeviceChange**](https://msdn.microsoft.com/library/windows/hardware/ff549625)
[**IoSetDeviceInterfaceState**](https://msdn.microsoft.com/library/windows/hardware/ff549700)
[**IoSetDevicePropertyData**](https://msdn.microsoft.com/library/windows/hardware/ff549704)
[**IoUnregisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff550398)
[**IoUnregisterPlugPlayNotificationEx**](https://msdn.microsoft.com/library/windows/hardware/ff550404)
[**IoUnregisterShutdownNotification**](https://msdn.microsoft.com/library/windows/hardware/ff550409)
[**IoUpdateShareAccess**](https://msdn.microsoft.com/library/windows/hardware/ff550412)
[**IoWMIAllocateInstanceIds**](https://msdn.microsoft.com/library/windows/hardware/ff550429)
[**IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)
[**KeDelayExecutionThread**](https://msdn.microsoft.com/library/windows/hardware/ff551986)
[**KeInitializeSemaphore**](https://msdn.microsoft.com/library/windows/hardware/ff552150)
[**KeQueryPriorityThread**](https://msdn.microsoft.com/library/windows/hardware/ff553062)
[**KeQueryRuntimeThread**](https://msdn.microsoft.com/library/windows/hardware/ff553065)
[**KeRevertToUserAffinityThreadEx**](https://msdn.microsoft.com/library/windows/hardware/ff553190)
[**KeSetSystemAffinityThread**](https://msdn.microsoft.com/library/windows/hardware/ff553267)
[**KeSetSystemGroupAffinityThread**](https://msdn.microsoft.com/library/windows/hardware/ff553275)
[**MmGetSystemRoutineAddress**](https://msdn.microsoft.com/library/windows/hardware/ff554563)
[**PsGetVersion**](https://msdn.microsoft.com/library/windows/hardware/ff559941)
[**PsRemoveLoadImageNotifyRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff559949)
[**PsSetCreateProcessNotifyRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff559951)
[**PsSetCreateProcessNotifyRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff559953)
[**PsSetCreateThreadNotifyRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff559954)
[**PsSetLoadImageNotifyRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff559957)
[**PsTerminateSystemThread**](https://msdn.microsoft.com/library/windows/hardware/ff559959)
[**SeAccessCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563674)
[**SeAssignSecurity**](https://msdn.microsoft.com/library/windows/hardware/ff563676)
[**SeDeassignSecurity**](https://msdn.microsoft.com/library/windows/hardware/ff563716)
[**SeSinglePrivilegeCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563740)
[**SeValidSecurityDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff563793)
[**ZwAllocateLocallyUniqueId**](https://msdn.microsoft.com/library/windows/hardware/ff566415)
[**ZwAllocateVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566416)
[**ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)
[**ZwCommitComplete**](https://msdn.microsoft.com/library/windows/hardware/ff566418)
[**ZwCommitEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff566419)
[**ZwCommitTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff566420)
[**ZwCreateDirectoryObject**](https://msdn.microsoft.com/library/windows/hardware/ff566421)
[**ZwCreateEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff566422)
[**ZwCreateEvent**](https://msdn.microsoft.com/library/windows/hardware/ff566423)
[**ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424)
[**ZwCreateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566425)
[**ZwCreateKeyTransacted**](https://msdn.microsoft.com/library/windows/hardware/ff566426)
[**ZwCreateResourceManager**](https://msdn.microsoft.com/library/windows/hardware/ff566427)
[**ZwCreateTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff566429)
[**ZwCreateTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff566430)
[**ZwDeleteFile**](https://msdn.microsoft.com/library/windows/hardware/ff566435)
[**ZwDeleteKey**](https://msdn.microsoft.com/library/windows/hardware/ff566437)
[**ZwDeleteValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff566439)
[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)
[**ZwDuplicateToken**](https://msdn.microsoft.com/library/windows/hardware/ff566446)
[**ZwEnumerateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566447)
[**ZwEnumerateTransactionObject**](https://msdn.microsoft.com/library/windows/hardware/ff566450)
[**ZwEnumerateValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff566453)
[**ZwFlushBuffersFile**](https://msdn.microsoft.com/library/windows/hardware/ff566454)
[**ZwFreeVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566460)
[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)
[**ZwGetNotificationResourceManager**](https://msdn.microsoft.com/library/windows/hardware/ff566467)
[**ZwLoadDriver**](https://msdn.microsoft.com/library/windows/hardware/ff566470)
[**ZwLockFile**](https://msdn.microsoft.com/library/windows/hardware/ff566474)
[**ZwMakeTemporaryObject**](https://msdn.microsoft.com/library/windows/hardware/ff566477)
[**ZwMapViewOfSection**](https://msdn.microsoft.com/library/windows/hardware/ff566481)
[**ZwNotifyChangeKey**](https://msdn.microsoft.com/library/windows/hardware/ff566488)
[**ZwOpenDirectoryObject**](https://msdn.microsoft.com/library/windows/hardware/ff566492)
[**ZwOpenEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567008)
[**ZwOpenEvent**](https://msdn.microsoft.com/library/windows/hardware/ff567009)
[**ZwOpenFile**](https://msdn.microsoft.com/library/windows/hardware/ff567011)
[**ZwOpenKey**](https://msdn.microsoft.com/library/windows/hardware/ff567014)
[**ZwOpenKeyEx**](https://msdn.microsoft.com/library/windows/hardware/ff567015)
[**ZwOpenKeyTransacted**](https://msdn.microsoft.com/library/windows/hardware/ff567018)
[**ZwOpenKeyTransactedEx**](https://msdn.microsoft.com/library/windows/hardware/ff567020)
[**ZwOpenProcess**](https://msdn.microsoft.com/library/windows/hardware/ff567022)
[**ZwOpenProcessTokenEx**](https://msdn.microsoft.com/library/windows/hardware/ff567024)
[**ZwOpenResourceManager**](https://msdn.microsoft.com/library/windows/hardware/ff567026)
[**ZwOpenSection**](https://msdn.microsoft.com/library/windows/hardware/ff567029)
[**ZwOpenSymbolicLinkObject**](https://msdn.microsoft.com/library/windows/hardware/ff567030)
[**ZwOpenThreadTokenEx**](https://msdn.microsoft.com/library/windows/hardware/ff567032)
[**ZwOpenTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff567033)
[**ZwOpenTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff567035)
[**ZwPowerInformation**](https://msdn.microsoft.com/library/windows/hardware/dn957454)
[**ZwPrepareComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567037)
[**ZwPrepareEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567039)
[**ZwPrePrepareComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567040)
[**ZwPrePrepareEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567044)
[**ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)
[**ZwQueryEaFile**](https://msdn.microsoft.com/library/windows/hardware/ff961907)
[**ZwQueryFullAttributesFile**](https://msdn.microsoft.com/library/windows/hardware/ff567049)
[**ZwQueryInformationEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567051)
[**ZwQueryInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567052)
[**ZwQueryInformationResourceManager**](https://msdn.microsoft.com/library/windows/hardware/ff567054)
[**ZwQueryInformationToken**](https://msdn.microsoft.com/library/windows/hardware/ff567055)
[**ZwQueryInformationTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff567057)
[**ZwQueryInformationTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff567058)
[**ZwQueryKey**](https://msdn.microsoft.com/library/windows/hardware/ff567060)
[**ZwQueryObject**](https://msdn.microsoft.com/library/windows/hardware/ff567062)
[**ZwQueryQuotaInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567064)
[**ZwQuerySecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567066)
[**ZwQuerySymbolicLinkObject**](https://msdn.microsoft.com/library/windows/hardware/ff567068)
[**ZwQueryValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567069)
[**ZwQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567070)
[**ZwReadFile**](https://msdn.microsoft.com/library/windows/hardware/ff567072)
[**ZwReadOnlyEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567074)
[**ZwRecoverEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567075)
[**ZwRecoverTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff567079)
[**ZwRollbackComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567081)
[**ZwRollbackEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567083)
[**ZwRollbackTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff567086)
[**ZwRollforwardTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff567089)
[**ZwSetEaFile**](https://msdn.microsoft.com/library/windows/hardware/ff961908)
[**ZwSetInformationEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567094)
[**ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096)
[**ZwSetInformationThread**](https://msdn.microsoft.com/library/windows/hardware/ff567101)
[**ZwSetInformationToken**](https://msdn.microsoft.com/library/windows/hardware/ff567102)
[**ZwSetInformationTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff567104)
[**ZwSetQuotaInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567105)
[**ZwSetSecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567106)
[**ZwSetValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567109)
[**ZwSetVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567112)
[**ZwSinglePhaseReject**](https://msdn.microsoft.com/library/windows/hardware/ff567113)
[**ZwTerminateProcess**](https://msdn.microsoft.com/library/windows/hardware/ff567115)
[**ZwUnloadDriver**](https://msdn.microsoft.com/library/windows/hardware/ff567117)
[**ZwUnlockFile**](https://msdn.microsoft.com/library/windows/hardware/ff567118)
[**ZwUnmapViewOfSection**](https://msdn.microsoft.com/library/windows/hardware/ff567119)
[**ZwWriteFile**](https://msdn.microsoft.com/library/windows/hardware/ff567121)
 

 





