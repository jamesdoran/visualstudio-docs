---
title: "CPU and Windows Counters | Microsoft Docs"
description: CPU (hardware) and Windows (software) counters provide performance data. Learn how to view them and how to collect data from them. 
ms.custom: SEO-VS-2020
ms.date: "11/04/2016"
ms.topic: "conceptual"
f1_keywords:
  - "vs.performance.property.counters"
helpviewer_keywords:
  - "Windows counters in Profiling Tools"
  - "CPU counters in Profiling Tools"
author: "mikejo5000"
ms.author: "mikejo"
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: 'vs-2017'
ms.workload:
  - "multiple"
---
# CPU and Windows counters

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

The Visual Studio Profiler enables you to collect performance data that was generated by the operating system (Windows counters) and performance data that was generated by the processor unit (CPU counters).

> [!NOTE]
> Enhanced security features in Windows 8 and Windows Server 2012 required significant changes in the way the Visual Studio profiler collects data on these platforms. UWP apps also require new collection techniques. See [Performance Tools on Windows 8 and Windows Server 2012 applications](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md).

## Windows counters

Windows counters are part of the Windows diagnostic infrastructure that provides information about the performance of the operating system or an application, a service, or a driver. Windows counters depend on the configuration of the current computer and might not be available on other computers. Windows performance counters are collected in profiling data files as profiling marks, which can then be used to filter views and reports.

## CPU counters

CPU counters are a feature of the computer's CPU that store the count of hardware-related events. When you collect CPU counter data by using the instrumentation profiling method, the data is appended to the data for functions and modules. You can collect multiple CPU counters using the instrumentation method. When you use the sampling method, you select one counter to use as the event to be sampled.

Performance counters are CPU-specific. Different models and versions of a CPU can have significantly different configuration settings to enable the same performance counter. [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] Profiler portable events decouple some common performance counters from specific processors and enable you to collect or sample generic performance events.

If you want to count a particular event when you use the profiler, for example, L2 cache misses, you can build a performance session around that event sender. You can do this on any CPU with an L2 cache. The performance session can be moved from platform to platform without modification.

The Visual Studio profiler continues to support particular events for a specific platform. For example, a developer on a Pentium 4 platform might want to count events that are specific to the NetBurst architecture. This event is not portable, but still available to the developer for a specific performance session on a specific platform.

## Portable and platform events

Portable events are a group of CPU counters that are not specific to a specific processor. All other CPU counters are called platform events, and might not be supported on various platforms.

 Counters for both portable and platform events are defined in .*xml* files, where specific values that are related to the counters are provided. There are multiple files for different CPUs, because data for Intel and AMD CPUs, for example, are different. The [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] Profiler uses this information to present appropriate counters, both portable and platform, to the user for performance measurement.

### Portable events

Portable events contain the following events:

**General Events**

|Event Name|Event Description|
|----------------|-----------------------|
|Instructions Retired|Indicates the number of instructions that executed until the event is completed.|
|Non Halted Cycles|Indicates only those cycles in which the processor is not stopped, for example, waiting for I/O.|

**Front End Events**

|Event Name|Event Description|
|----------------|-----------------------|
|ITLB Misses|Indicates the number of Instruction Translation Look-aside Buffer lookups that resulted in a miss.|

**Branch Events**

|Event Name|Event Description|
|----------------|-----------------------|
|Branches Retired|Indicates the number of branch instructions executed until the event is completed.|
|Mis-predicted Branches|Indicates mis-predicted branches that occur because the processor predicted an incorrect path. Mis-predicted branches affect performance because the processor must discard all the work done and start again on a correct path.|

**Memory Events:**

|Event Name|Event Description|
|----------------|-----------------------|
|L2 Cache Read Misses|Indicates the number of second level cache read misses.|
|L2 Cache Read References|Indicates the number of second level cache read references. It includes load misses and read for ownership (RFO) misses and hits.|

## View available counters

You can list the available CPU counters in the Visual Studio IDE on in a Command Prompt window.

### Visual Studio UI

To list the available counters on a computer in the Visual Studio IDE, you must have a profiler performance session open in Performance Explorer.

#### To view a list of a list of all CPU counters that are supported on the current platform

1. In Performance Explorer, right-click the performance session and then click **Properties**.

2. Do one of the following:

   - Click **Sampling**, and then select **Performance counter** from the **Sample** event list. The CPU counters are listed in **Available performance counters**.

      **Note** Click **Cancel** to return to the previous sampling configuration.

     -or-

   - Select **CPU Counters**, and then select **Collect CPU Counters**. The CPU counters are listed in **Available counters**.

      **Note** Click **Cancel** to return to the previous counter collection configuration.

#### To view a list of a list of Window counters that are supported on the current platform

1. In Performance Explorer, right-click the performance session and then click **Properties**.

2. Click **Windows Counters**.

3. Select **Collect Windows Counters**.

4. From the **Counter Category** list, select a counter group. The Windows counter for the group is displayed in the list box.

     **Note:** Click **Cancel** to return to the previous counter collection configuration.

### Command line

Using the [VSPerfCmd](../profiling/vsperfcmd.md) command line tool, you can list the CPU counters that are available on a computer from the command line.

#### To list of CPU counters that are supported on the current platform

1. Open a command prompt window.

2. Type

     **\<Visual Studio Performance Tools Directory>\VSPerfCmd /querycounters**

     where *\<Visual Studio Performance Tools Directory>* is the path to the Performance Tools directory of your Visual Studio installation. To get the path to the performance tools, see [Specify the path to command line tools](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md).

## See also

- [Overviews](../profiling/overviews-performance-tools.md)
- [How to: Choose sampling events](../profiling/how-to-choose-sampling-events.md)
- [How to: Collect CPU counter data](../profiling/how-to-collect-cpu-counter-data.md)
- [How to: Collect Windows counter data](../profiling/how-to-collect-windows-counter-data.md)
