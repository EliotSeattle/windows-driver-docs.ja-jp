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
ms.openlocfilehash: 03d1825bf8bd1dc62ddf2c86eb2b63215a287fc1
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393677"
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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>PowerIrpDDIs</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**ExIsProcessorFeaturePresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exisprocessorfeaturepresent)
[**ExRaiseAccessViolation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exraiseaccessviolation)
[**ExRaiseDatatypeMisalignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exraisedatatypemisalignment)
[**ExUuidCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exuuidcreate)
[**HalExamineMBR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-halexaminembr)
[**HalGetInterruptVector**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))
[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)
[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildsynchronousfsdrequest)
[**IoCheckShareAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocheckshareaccess)
[**IoConnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterrupt)
[**IoCreateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatecontroller)
[**IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatefile)
[**IoCreateSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatesymboliclink)
[**IoCreateSynchronizationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatesynchronizationevent)
[**IoCreateUnprotectedSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreateunprotectedsymboliclink)
[**IoDeleteController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iodeletecontroller)
[**IoDeleteSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletesymboliclink)
[**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodetachdevice)
[**IoDisconnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterrupt)
[**IoGetConfigurationInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iogetconfigurationinformation)
[**IoGetDeviceInterfaceAlias**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceinterfacealias)
[**IoGetDeviceInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceinterfaces)
[**IoGetDeviceNumaNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdevicenumanode)
[**IoGetDeviceObjectPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)
[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)
[**IoGetDevicePropertyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdevicepropertydata)
[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)
[**IoGetFileObjectGenericMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iogetfileobjectgenericmapping)
[**IoInitializeTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializetimer)
[**IoIsWdmVersionAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioiswdmversionavailable)
[**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)
[**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey)
[**IoRegisterBootDriverReinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioregisterbootdriverreinitialization)
[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)
[**IoRegisterDriverReinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioregisterdriverreinitialization)
[**IoRegisterLastChanceShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterlastchanceshutdownnotification)
[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterplugplaynotification)
[**IoRegisterShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregistershutdownnotification)
[**IoRemoveShareAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioremoveshareaccess)
[**IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioreportdetecteddevice)
[**IoReportTargetDeviceChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioreporttargetdevicechange)
[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)
[**IoSetDevicePropertyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdevicepropertydata)
[**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iounregisterplugplaynotification)
[**IoUnregisterPlugPlayNotificationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iounregisterplugplaynotificationex)
[**IoUnregisterShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iounregistershutdownnotification)
[**IoUpdateShareAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioupdateshareaccess)
[**IoWMIAllocateInstanceIds**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiallocateinstanceids)
[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)
[**KeDelayExecutionThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kedelayexecutionthread)
[**KeInitializeSemaphore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializesemaphore)
[**KeQueryPriorityThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequeryprioritythread)
[**KeQueryRuntimeThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequeryruntimethread)
[**KeRevertToUserAffinityThreadEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereverttouseraffinitythreadex)
[**KeSetSystemAffinityThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetsystemaffinitythread)
[**KeSetSystemGroupAffinityThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetsystemgroupaffinitythread)
[**MmGetSystemRoutineAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetsystemroutineaddress)
[**PsGetVersion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-psgetversion)
[**PsRemoveLoadImageNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psremoveloadimagenotifyroutine)
[**PsSetCreateProcessNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine)
[**PsSetCreateProcessNotifyRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreateprocessnotifyroutineex)
[**PsSetCreateThreadNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine)
[**PsSetLoadImageNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetloadimagenotifyroutine)
[**PsTerminateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-psterminatesystemthread)
[**SeAccessCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-seaccesscheck)
[**SeAssignSecurity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-seassignsecurity)
[**SeDeassignSecurity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-sedeassignsecurity)
[**SeSinglePrivilegeCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-sesingleprivilegecheck)
[**SeValidSecurityDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-sevalidsecuritydescriptor)
[**ZwAllocateLocallyUniqueId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-zwallocatelocallyuniqueid)
[**ZwAllocateVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566416)
[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)
[**ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitcomplete)
[**ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitenlistment)
[**ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)
[**ZwCreateDirectoryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject)
[**ZwCreateEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateenlistment)
[**ZwCreateEvent**](https://msdn.microsoft.com/library/windows/hardware/ff566423)
[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)
[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)
[**ZwCreateKeyTransacted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekeytransacted)
[**ZwCreateResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateresourcemanager)
[**ZwCreateTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransaction)
[**ZwCreateTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransactionmanager)
[**ZwDeleteFile**](https://msdn.microsoft.com/library/windows/hardware/ff566435)
[**ZwDeleteKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletekey)
[**ZwDeleteValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwdeletevaluekey)
[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)
[**ZwDuplicateToken**](https://msdn.microsoft.com/library/windows/hardware/ff566446)
[**ZwEnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwenumeratekey)
[**ZwEnumerateTransactionObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntenumeratetransactionobject)
[**ZwEnumerateValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwenumeratevaluekey)
[**ZwFlushBuffersFile**](https://msdn.microsoft.com/library/windows/hardware/ff566454)
[**ZwFreeVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566460)
[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)
[**ZwGetNotificationResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntgetnotificationresourcemanager)
[**ZwLoadDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwloaddriver)
[**ZwLockFile**](https://msdn.microsoft.com/library/windows/hardware/ff566474)
[**ZwMakeTemporaryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwmaketemporaryobject)
[**ZwMapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwmapviewofsection)
[**ZwNotifyChangeKey**](https://msdn.microsoft.com/library/windows/hardware/ff566488)
[**ZwOpenDirectoryObject**](https://msdn.microsoft.com/library/windows/hardware/ff566492)
[**ZwOpenEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopenenlistment)
[**ZwOpenEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenevent)
[**ZwOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntopenfile)
[**ZwOpenKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkey)
[**ZwOpenKeyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkeyex)
[**ZwOpenKeyTransacted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkeytransacted)
[**ZwOpenKeyTransactedEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkeytransactedex)
[**ZwOpenProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ntopenprocess)
[**ZwOpenProcessTokenEx**](https://msdn.microsoft.com/library/windows/hardware/ff567024)
[**ZwOpenResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopenresourcemanager)
[**ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection)
[**ZwOpenSymbolicLinkObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensymboliclinkobject)
[**ZwOpenThreadTokenEx**](https://msdn.microsoft.com/library/windows/hardware/ff567032)
[**ZwOpenTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopentransaction)
[**ZwOpenTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopentransactionmanager)
[**ZwPowerInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpowerinformation)
[**ZwPrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreparecomplete)
[**ZwPrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepareenlistment)
[**ZwPrePrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepreparecomplete)
[**ZwPrePrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreprepareenlistment)
[**ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)
[**ZwQueryEaFile**](https://msdn.microsoft.com/library/windows/hardware/ff961907)
[**ZwQueryFullAttributesFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwqueryfullattributesfile)
[**ZwQueryInformationEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationenlistment)
[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile)
[**ZwQueryInformationResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationresourcemanager)
[**ZwQueryInformationToken**](https://msdn.microsoft.com/library/windows/hardware/ff567055)
[**ZwQueryInformationTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationtransaction)
[**ZwQueryInformationTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationtransactionmanager)
[**ZwQueryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwquerykey)
[**ZwQueryObject**](https://msdn.microsoft.com/library/windows/hardware/ff567062)
[**ZwQueryQuotaInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567064)
[**ZwQuerySecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567066)
[**ZwQuerySymbolicLinkObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwquerysymboliclinkobject)
[**ZwQueryValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwqueryvaluekey)
[**ZwQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567070)
[**ZwReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntreadfile)
[**ZwReadOnlyEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntreadonlyenlistment)
[**ZwRecoverEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverenlistment)
[**ZwRecoverTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecovertransactionmanager)
[**ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackcomplete)
[**ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackenlistment)
[**ZwRollbackTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbacktransaction)
[**ZwRollforwardTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollforwardtransactionmanager)
[**ZwSetEaFile**](https://msdn.microsoft.com/library/windows/hardware/ff961908)
[**ZwSetInformationEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsetinformationenlistment)
[**ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntsetinformationfile)
[**ZwSetInformationThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-zwsetinformationthread)
[**ZwSetInformationToken**](https://msdn.microsoft.com/library/windows/hardware/ff567102)
[**ZwSetInformationTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsetinformationtransaction)
[**ZwSetQuotaInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567105)
[**ZwSetSecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567106)
[**ZwSetValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwsetvaluekey)
[**ZwSetVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567112)
[**ZwSinglePhaseReject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsinglephasereject)
[**ZwTerminateProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-zwterminateprocess)
[**ZwUnloadDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwunloaddriver)
[**ZwUnlockFile**](https://msdn.microsoft.com/library/windows/hardware/ff567118)
[**ZwUnmapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwunmapviewofsection)
[**ZwWriteFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntwritefile)
 

 





