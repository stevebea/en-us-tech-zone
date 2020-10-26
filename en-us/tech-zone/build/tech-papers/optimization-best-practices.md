---
layout: doc
---

# Optimization best practices for VDI / RDS workloads

## Contributors

**Author:** [Martin Zugec](https://twitter.com/MartinZugec)

User experience is key to building Citrix environments that are successful, loved by the end users and sustainable over long term. In today's modern workspace, users have access to a wide range of personal devices - mobile phones, tablets, laptops, consoles - and experience with Citrix environments is compared against these native environments. When user experience in the workplace is poor, users experience frustration and low productivity and are often looking to use non-sanctioned external solutions to get things done. Successful Citrix projects are boosting user productivity and not hampering it.

One attribute that is shared by various successful projects that we have observed over the years is focus on user experience - not only relying on a quantifiable data (length of logon etc.), but directly interacting with your end users and listening to their feedback.

Optimization is in many aspects similar to security - it should to be an ongoing process with incremental improvements. Following tech paper is written in a similar style - we are planning to review / update it on a regular basis. If you have any questions / comments or suggestions for new content, please let us know by [submitting your idea here](/en-us/tech-zone/about.html).

## Why We Optimize

Hopefully you are optimizing your environment as a pro-active activity and not as reaction to user complains. Most common benefits of optimizing your images are:

-  Increased User Density - by optimizing your images, you can have more users on the same hardware. Even by applying the minimum set of optimizations, you can greatly improve scalability numbers in your environment.
-  Improved User Experience - faster printing, opening a file dialog, dragging window on the screen without any slowdowns - these are few examples of improvements that are greatly appreciated by end users.
-  Improved Logon and Launch Times - in some industries (most notably healthcare), time it takes to launch the application is extremely important metric to follow. For many environments, every seconds count and can make a huge difference for user experience.
-  Improved Security - by removing components that are not needed, you are reducing the attack surface. Another very important security aspect to keep on your mind - with better user experience, you can prevent potential data loss as users will not resort to using "shadow IT" solutions.

## How To Optimize

Problem with defining and delivering a good user experience is that user experience (or UX) is that it isn’t particularly an objective definition. UX is a holistic metric, encompassing the user’s overall feeling of satisfaction or engagement with not just one, but all of the systems at their disposal. UX can vary from user to user and department to department depending on how they interact with applications, and to what degree. Understanding how your users are feeling about the “experience” is vital, yet pinning it down to a specific "rating" can be incredibly difficult.

### Focus on Priorities

This can be ideally achieved by listening to your end users. Find out what you could do to improve their productivity, their pain points and priorities. Make sure that you are solving the right problem and then find the best way to do it.

For example, if your goal is to improve logon times, start by analyzing which part of logon process takes most time. If your GPO processing takes only 2-3 seconds, but overall logon times is 3 minutes, it should probably not be your priority.

Before your start optimizing, it is important to analyze your environment, understand the bottlenecks and approach the problem systematically.

### Measuring Impact

Measuring user experience is not simple task. However, if you are planning to optimize your environment, you should have a methods to measure the impact of your changes. Historically, many optimizations that were useful in the past have become obsolete (or even worse, started having a negative impact) in newer versions of Windows. It is important to measure key performance indicators (KPI) before and after your optimizations.

While it is difficult, it is possible to define to a certain degree the current level of user experience being delivered to users in the environment. Certain technical solutions can aggregate key performance indicators together to produce a "UX" metric which serves as an indicator of the current level. They normally work by combining together a set of KPIs that are used to extrapolate a specific UX reading. The KPIs involved usually include things such as, but not limited to:-

-  Logon times
-  Application launch times
-  Key application interactions (e.g. opening a document from a dialog box, entering data, etc.)
-  Common admin tasks (e.g. running a report, exporting data, etc.)
-  Printing
  
Being able to define the UX metric also points us to another bugbear of modern IT environments – the focus of monitoring. Traditionally, monitoring of systems concentrated solely on back-end infrastructure – looking at databases, storage, networks and servers. Now that the performance on the client end – the front end – is also considered equally important, the focus of our monitoring needs to shift to encompass the whole environment, rather than just the infrastructure. This level of monitoring is also vitally important in any upgrade project – allowing baselining of the UX in both old and new environments to assess any performance improvement or degradation.

### User Acceptance Testing

This tip is critical when your focus is on density or security. You should always make sure that your optimizations do not have negative impact on user experience and implement a proper change management procedures.

## Windows Operating System

Similar to security hardening, most optimizations are focused on underlying operating system rather than actual Citrix components. With agile development and multiple releases every year, you might get a lot of benefits by simply switching to another build of Windows (or components such as Citrix VDA).

Windows has been very successful in last few decades in building an operating system that is easy to use, works out of the box and can adapt to different situations. Whether you are professional designer, programmer, gamer, video enthusiast or task worker, you can use almost identical Windows build. Same Windows build is used for physical tablets and virtualized machines running in cloud. As a result, there are many components of Windows operating systems that are not required for virtualized machines.

Optimizing Windows operating system is primarily focused on removing components that are not required for virtualized workloads. We do **not** include specific recommendations in this document - instead, these recommendations are automated with [Citrix Optimizer](#citrix-optimizer).

### Built-in Applications

Starting with Windows 10, Microsoft has introduced new Universal Windows Platform. Purpose of this platform is to develop modern and secure universal applications that can be used on Windows 10, Xbox, HoloLens and other devices.

Most UWP applications are not used in enterprise environments and they have significant impact on performance of operating system, from logon times to CPU, memory and storage usage. It is recommended to carefully review UWP applications that you need to use and configure provisioning.

### Services

Windows operating system contains many services that are not required in virtualized environments. While historically disabling unnecessary services has been one of the most popular optimizations, the impact has been minimal in the recent Windows builds. Even if it is minimal, it is cumulative if you disable dozens of services.

### Scheduled Tasks

Historically, scheduled tasks has been mostly running on a regular basis (scheduled) or specific events, such as startup or user logon. In Windows Vista, capabilities of scheduled tasks has been greatly expanded with introduction of Task Scheduler 2.0. This new implementation allowed Microsoft and 3rd party vendors to add hundreds of new scheduled tasks, while minimizing the performance impact they can have on operating system.

### Active Setup

Active Setup is a Windows functionality to execute commands when user logs on to machine for a first time. Active Setup has been used mostly for old operating systems, such as Windows 2000 and Windows XP, but has been mostly abandoned in newer releases. It is still available for backwards compatibility.

It is executed by Explorer.exe, therefore it is skipped in environments like RDS or Citrix Virtual Apps where full desktop is not loaded.

## Group Policies

Group Policy is one of the areas that proves to hold the key to a lot of logon delays. User-level Group Policies are often quite extensive and apply a huge amount of customizations based on a wide variety of parameters.

### Structuring

Most administrators are diligent about producing a “one GPO, one setting” relationship that looks very neat and tidy. The beauty of this approach is that it makes troubleshooting very easy – simply disable the link to each GPO, retest, and it will soon be obvious which of your policy settings is causing problems.

Unfortunately – this isn’t the most efficient way of actually processing GPOs. Loading lots of settings into a single, monolithic policy object is more efficient when it comes to logon times. I know this is hideously annoying, because you can’t troubleshoot as effectively, but it is what it is. If you want the fastest possible logon times, then combine all GPOs for each OU into a single policy object.

It is important to balance out the adverse effects on your management capability against what you’re saving in logon times. In these cases, having a proper client monitoring tool that can measure each part of your logon process very precisely is incredibly vital (hence my mentioning of it in just about every presentation I give!) In most cases, you will probably find that grouping together large numbers of policy objects that are similar in operation can give you the best savings without trading off too heavily in administration overhead. For instance – put Microsoft Office settings all in one GPO, put browser settings in another, etc. The ratio of GPOs to settings is something that you will have to balance out to give yourself the best possible all-round experience.

This is a fairly simplistic view of what can be a very complex area of your environment, however, and dependent on how your GPOs are set up, balancing the functionality against the size is something that may need extra attention. For a very detailed dive into GPO processing and design, see [this link](https://docs.microsoft.com/en-us/previous-versions/technet-magazine/cc137720(v=msdn.10)).

### Filtering

Filtering can have a dramatic effect on GPO processing. You can filter in several ways – through standard Security Filtering, a WMI filter, or through Item-Level Targeting (specifically on Group Policy Preferences).

WMI filters can be the most harmful, as they can be written by the user and can contain many different queries. In general, try and keep WMI filters short and to the point, and especially avoid using LDAP queries, as these seem to be the most costly in terms of processing time. In my environments I try, wherever possible, to avoid WMI filters altogether, although this may not be possible for everyone.

Item-Level Targeting can also introduce delays into the logon process. Again, it depends somewhat upon the type of filter selected – my testing indicates that OU, LDAP Query, Domain, Site or Computer Group filters have the most overhead in processing time. Again, if possible I would try to avoid using ILT, although that sometimes it isn’t possible to remove entirely.

Security Filtering has for a long time been the most efficient way of filtering GPOs because it generally uses user or security group membership, details of which are contained within the user’s local security token. However, for a few years now using Security Filtering by user or group also performs some execution in the computer context, meaning that the Domain Computers group also has to be specified on the security filter to allow it to be filtered by user or group. This change, made for security purposes, also makes processing slightly more inefficient, meaning that even this method of filtering comes with a slight overhead.

Ideally, it would be prudent to apply GPOs without filtering and apply them simply to the relevant OUs without any specific targeting. This would allow for the most efficient processing – but unfortunately very few environments are simple enough to allow this kind of direct targeting. Try and get your filtering as close to vanilla as possible.

### Asynchronous and Synchronous Processing

### Disabling User/Computer Policies

In a similar sort of vein, it has for a long time been a common “best practice” for administrators to try and improve Group Policy processing by disabling Computer settings for GPOs that only contain User settings, and disabling User settings for GPOs that only contain Computer settings.

Actually – performing this step not only doesn’t have any effect on overall processing time, making it a completely useless exercise, it also encourages administrators to split GPOs into “user-only” and “computer-only”, which actually increases logon times because (as per the section above), it increases the number of GPOs required. So this is a redundant setting – avoid using it, leave all GPOs set to Enabled. In general, I’d use this only for troubleshooting, which you will soon be glad of, especially if you implement the first GPO tip given above.

### Merge vs Replace Loopback

## Tools

### Citrix Optimizer

### Citrix Workspace Environment Management

### Citrix Director

### Citrix Profile Management

## Profiles and Logons

### Logon Scripts

### Profile Types

### Folder Redirection

### Profile Size

## Pre-loading and Caching

### Session Pre-launch

### Session Lingering

### Automatic Logon

### Application Pre-launch

## Miscellaneous

### Perceived Performance

### Antivirus Configuration

### Web Browsers

## Summary

## Reset the Citrix ADC lights out management (LOM)
