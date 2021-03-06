---
title: Attachments
sidebar_order: 7
---
# Event Attachments

Besides crash reports, Sentry can optionally store additional files uploaded in the same request, such as log files, as event attachments. Attachments allow the files within a crash to not only upload to Sentry, but also persist for further investigation. You can use a higher-level SDK for platforms with built-in support for native crashes, or generate and upload attachments using the API:

- [Native C/C++](/platforms/native/)
- [Electron](/platforms/javascript/electron/)
- [Minidump endpoint](/platforms/native/minidump/)

To receive symbolicated stack traces, you have to upload debug information to Sentry. Unless the option to store crash reports is enabled, Sentry will use the crash reports only to create the event, then will drop the files. For more information, see [Debug Information Files](/workflow/debug-files/).

## Storage and Quota Impact

Attachments persist for 30 days; if your total storage included in your quota is exceeded, attachments will not be stored. You can delete attachments or their containing events at any time. Deleting an attachment does not affect your quota - Sentry counts an attachment toward your quota as soon as it is stored. 

Learn more about how attachments impact your [quota](/accounts/quotas/).

## Crash Reports and Privacy

Crash reports may contain sensitive information about the target system, such as environment variables, local pathnames, or in-memory representations of input fields, including passwords. By default, Sentry only uses crash report files to create events and immediately drops them. All sensitive information is stripped from the resulting events.

All other types of attachments, such as log files or screenshots, are stored for 30 days when sent to Sentry. Note that Sentry does not apply data scrubbing to attachments.

### Enabling Crash Report Storage

You can enable *Store Native Crash Reports* in your organization's **Security and Privacy Settings**. By default, this setting is disabled. Determine the maximum number of crash reports that will be stored per issue; disabled, unlimited, or maximum per issue:

[{% asset attachments/slide-bar-native-crashes.png alt="Attachments Example" %}]({% asset attachments/slide-bar-native-crashes.png @path %})

If you set a limit per issue, as in the example above, a limit of 10, Sentry will store the first 10 attachments associated with this issue, but drop any that follow. To make room for additional attachments, delete them. Sentry will then accept attachments until the limit is reached again.

### Access to Attachments

To limit access to attachments, navigate to your organization's **General Settings**, then select the *Attachments Access* dropdown to set appropriate access — any member of your organization, the organization billing owner, member, admin, manager, or owner. 

[{% asset attachments/attachments-access.png alt="Attachments Access" %}]({% asset attachments/attachments-access.png @path %})

By default, access is granted to all members when storage is enabled. If a member does not have access to the project, the ability to download an attachment is not available; the button will be greyed out in Sentry. The member may only view that an attachment is stored.

## Viewing Attachments

Attachments display on the bottom of the **Issue Details** page for the event that is shown.

[{% asset attachments/attachments-access-denied.png alt="Attachments Access Denied" %}]({% asset attachments/attachments-access-denied.png @path %})

Alternately, attachments also appear in the *Attachments* tab on the **Issue Details** page, where you can view the *Type* of attachment, as well as associated events. Click the Event ID to open the **Issue Details** of that specific event. 

[{% asset attachments/attachments-list-example.png alt="Attachments List Example" %}]({% asset attachments/attachments-list-example.png @path %})

If you chose to limit the number of crash reports per issue, you can show *Only Crash Reports*. This removes all other attachments from the list, which can be useful if the issue has accumulated a large number of events.